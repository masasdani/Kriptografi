/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package com.masasdani.kriptografi.util;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
import java.security.NoSuchAlgorithmException;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.security.Signature;
import java.util.Random;
import java.util.Vector;


/**
 *
 * @author masasdani
 * visit http://masasdani.com or http://mexez.wordpress.com
 * twitter @masasdani
 * facebook http://facebook.com/mexezdhanie
 *
 */
public abstract class Utilities {
   
    /**
     * Generates a random string, used for new key names
     * @param length The random string's length
     * @return Random string with the specified length
     */
    public static String generateRandomString(int length) {
        Random rnd = new Random(System.currentTimeMillis());
        String rand = new String("key");
        for(int x = 0; x < length; x++)
            rand += new String("" + (char)(rnd.nextInt(9)+48));
        return rand;
    }
   
    /**
     * Converts a byte array to a string representing it in hexadecimal format
     * @param in The byte array to convert to a string
     * @return Hexadecimal string representing the given byte array
     */
    public static String byteArrayToHexString(byte in[]) {
        byte ch = 0x00;
       
        int i = 0;
       
        if (in == null || in.length <= 0)
            return null;
       
        String pseudo[] = {"0", "1", "2",
        "3", "4", "5", "6", "7", "8",
        "9", "A", "B", "C", "D", "E",
        "F"};
       
        StringBuffer out = new StringBuffer(in.length * 2);
       
        while (i < in.length) {
            ch = (byte) (in[i] & 0xF0); // Strip off high nibble
            ch = (byte) (ch >>> 4); // shift the bits down
            ch = (byte) (ch & 0x0F); // must do this is high order bit is on!
            out.append(pseudo[ (int) ch]); // convert the nibble to a String Character
            ch = (byte) (in[i] & 0x0F); // Strip off low nibble
            out.append(pseudo[ (int) ch]); // convert the nibble to a String Character
            i++;
        }
       
        String rslt = new String(out);
       
        return rslt;
    }
   
   
    /**
     * Returns the md5 hash of an array of bytes
     * @param input The input of
     * @return The MD5 hash
     */
    public static byte [] md5(byte [] input) {
        try {
            java.security.MessageDigest md;
            md = java.security.MessageDigest.getInstance("MD5");
            md.update(input);
            return md.digest();
        } catch (NoSuchAlgorithmException ex) {
            ex.printStackTrace();
        }
       
        return null;
    }
   
    /**
     * Adds an MD5 checkum to the beginning of a byte stream
     * @param original The original byte stream
     * @return A new byte stream with an MD5 hash at it's start, and the original data following it
     */
    public static byte[] insertChecksum(byte [] original) {
        // Get the MD5 hash of the original file
        byte [] md5_hash = Utilities.md5(original);
       
        // Add the MD5 hash to the top of the original file
        byte [] original_plus_hash = new byte[original.length + md5_hash.length];
        int off = 0;
        // Insert MD5 hash at the start
        for(off = 0; off < md5_hash.length; off++)
            original_plus_hash[off] = md5_hash[off];
        // Insert original stream next to the MD5 hash
        for(int x = 0; x < original.length; x++)
            original_plus_hash[off+x] = original[x];
       
        return original_plus_hash;
    }
   
    /**
     * Partitions a byte stream into multiple chunks of a maximum size
     * @param original Original byte stream to be partitioned into chunks
     * @param chunk_size Maximum size of each data chunk
     * @return Vector with all the data chunks
     */
    public static Vector<byte []> partitionData(byte [] original, int chunk_size) {
        Vector <byte []> chunks = new Vector <byte []> ();
        int original_offset = 0;
        int chunk_offset = 0;
        while(original_offset < original.length) {
            byte [] chunk = chunk_size < (original.length - original_offset) ? new byte[chunk_size] : new byte[original.length - original_offset];
            for(chunk_offset = 0; chunk_offset < chunk_size && original_offset < original.length; original_offset++,chunk_offset++)
                chunk[chunk_offset] = original[original_offset];
            chunks.add(chunk);
        }
       
        return chunks;
    }
   
    /**
     * Merges a vector of data chunks back into one single chunk
     * @param chunks Vector of data chunks
     * @return Byte stream containing the merged data
     */
    public static byte[] mergeData(Vector <byte []> chunks) {
        // Allocate space for the merged data
        int size = 0;
        for(int x = 0; x < chunks.size(); x++)
            size += chunks.get(x).length;
        byte [] return_data = new byte[size];
       
        // Merge the data
        int offset = 0;
        for(int x = 0; x < chunks.size(); x++)
            for(int y = 0; y < chunks.get(x).length; y++,offset++)
                return_data[offset] = chunks.get(x)[y];
       
        return return_data;
    }
   
    /**
     * Extracts the MD5 hash from the beginning of the byte stream
     * @param original The data with the MD5 hash at it's start
     */
    public static byte [] extractMD5(byte [] original) {
        byte [] found_md5 = new byte[16];
        for(int x = 0; x < 16; x++)
            found_md5[x] = original[x];
        return found_md5;
    }
   
    /**
     * Returns the data that's in front of the MD5 hash
     * @param original Data with it's MD5 hash in front of it
     * @return Returns the data without it's MD5 hash in front of it
     */
    public static byte [] extractData(byte [] original) {
        byte [] found_data = new byte[original.length - 16];
        for(int x = 0; x < original.length - 16; x++)
            found_data[x] = original[x+16];
        return found_data;
    }
   
    public byte[] sign(String datafile, PrivateKey prvKey, String sigAlg) {
        try {
            Signature sig = Signature.getInstance(sigAlg);
            sig.initSign(prvKey);
            FileInputStream fis = new FileInputStream(datafile);
            byte[] dataBytes = new byte[1024];
            int nread = fis.read(dataBytes);
            while (nread > 0) {
                sig.update(dataBytes, 0, nread);
                nread = fis.read(dataBytes);
            };
            return sig.sign();
        } catch (Exception e){}
       
        return null;
    }
   
    public boolean verify(String datafile, PublicKey pubKey, String sigAlg, byte[] sigbytes) {
        try {
            Signature sig = Signature.getInstance(sigAlg);
            sig.initVerify(pubKey);
            FileInputStream fis = new FileInputStream(datafile);
            byte[] dataBytes = new byte[1024];
            int nread = fis.read(dataBytes);
            while (nread > 0) {
                sig.update(dataBytes, 0, nread);
                nread = fis.read(dataBytes);
            };
            return sig.verify(sigbytes);
        } catch(Exception e) {
        }
       
        return false;
    }
   
    /**
     * Makes true copy of an object (with a different pointer)
     *
     * @param o
     *            A serializable object instance
     * @return The object clone
     */
    public static Object clone(Serializable o) {
        try {
            ByteArrayOutputStream b = new ByteArrayOutputStream();
            ObjectOutputStream out;
            out = new ObjectOutputStream(b);
            out.writeObject(o);
            out.close();
            ByteArrayInputStream bi = new ByteArrayInputStream(b.toByteArray());
            ObjectInputStream in = new ObjectInputStream(bi);
            Object no = in.readObject();
            return no;
        } catch (IOException e) {
            System.err.println("ERROR: Input/Output exception whilst cloning an object.");
            e.printStackTrace();
            return null;
        } catch (ClassNotFoundException e) {
            System.err.println("ERROR: Unknown class found whilst cloning an object.");
            e.printStackTrace();
            return null;
        }
    }
   
    /**
     * Get the extension of a file.
     * @param f File from which the extension will be retrieved
     * @return Extension of the specified file
     */  
    public static String getExtension(File f) {
        String ext = null;
        String s = f.getName();
        int i = s.lastIndexOf('.');

        if (i > 0 &&  i < s.length() - 1) {
            ext = s.substring(i+1).toLowerCase();
        }
        return ext;
    }
}
