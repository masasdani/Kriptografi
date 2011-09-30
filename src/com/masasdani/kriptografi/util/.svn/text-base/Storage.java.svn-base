/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package com.masasdani.kriptografi.util;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
public abstract class Storage {
    
    /**
     * Returns an array of bytes with the content of a file
     * @param path The path for the file to be converted into an array of bytes
     * @return Array of bytes with the content of the file
     */
    public static byte[] readFile(String path) {
        try {
            int length = (int) new File(path).length();
            byte [] buffer = new byte[length];
            DataInputStream reader = new DataInputStream(new FileInputStream(path));
            reader.read(buffer,0,length);
            reader.close();
            return buffer;
        } catch (FileNotFoundException ex) {
            ex.printStackTrace();
        } catch (IOException ex) {
            ex.printStackTrace();
        }
        return null;
    }
    
    /**
     * Saves an array of bytes to a file
     * @param path Path to the file where the bytes will be saved
     * @param content Array of bytes to save to the file
     */
    public static void saveFile(String path, byte [] content) {
        try {
            DataOutputStream writer = new DataOutputStream(new FileOutputStream(path));
            writer.write(content);
            writer.close();
        } catch (FileNotFoundException ex) {
            ex.printStackTrace();
        } catch (IOException ex) {
            ex.printStackTrace();
        }
    }
}
