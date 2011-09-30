/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package com.masasdani.kriptografi.util;

/**
 *
 * @author masasdani
 * visit http://masasdani.com or http://mexez.wordpress.com
 * twitter @masasdani
 * facebook http://facebook.com/mexezdhanie
 *
 */
public class StringUtil {
    //~ Instance/static variables .............................................

    private static final int BYTE_RANGE = (1 + Byte.MAX_VALUE)
                                          - Byte.MIN_VALUE;
    private static byte[] allBytes = new byte[BYTE_RANGE];
    private static char[] byteToChars = new char[BYTE_RANGE];

    //~ Initializers ..........................................................

    static {

        for (int i = Byte.MIN_VALUE; i <= Byte.MAX_VALUE; i++) {
            allBytes[i - Byte.MIN_VALUE] = (byte) i;
        }

        String allBytesString = new String(allBytes, 0, 
                                           Byte.MAX_VALUE - Byte.MIN_VALUE);

        for (int i = 0; i < (Byte.MAX_VALUE - Byte.MIN_VALUE); i++) {
            byteToChars[i] = allBytesString.charAt(i);
        }
    }



    /**
     * DOCUMENT ME!
     * 
     * @param buffer DOCUMENT ME!
     * @param startPos DOCUMENT ME!
     * @param length DOCUMENT ME!
     * @return DOCUMENT ME! 
     */
    public static final String toAsciiString3(byte[] buffer, int startPos, 
                                              int length) {

        char[] charArray = new char[length];
        int readpoint = startPos;

        for (int i = 0; i < length; i++) {
            charArray[i] = byteToChars[(int) buffer[readpoint]
                           - Byte.MIN_VALUE];
            readpoint++;
        }

        return new String(charArray);
    }

    /**
     * DOCUMENT ME!
     * 
     * @param buffer DOCUMENT ME!
     * @return DOCUMENT ME! 
     */
    public static final String toAsciiString(byte[] buffer) {

        return toAsciiString3(buffer, 0, buffer.length);
    }

    /**
     * DOCUMENT ME!
     * 
     * @param buffer DOCUMENT ME!
     * @param startPos DOCUMENT ME!
     * @param length DOCUMENT ME!
     * @return DOCUMENT ME! 
     */
    public static final String toAsciiString2(byte[] buffer, int startPos, 
                                              int length) {

        return new String(buffer, startPos, length);
    }

    /**
     * DOCUMENT ME!
     * 
     * @param buffer DOCUMENT ME!
     * @param startPos DOCUMENT ME!
     * @param length DOCUMENT ME!
     * @return DOCUMENT ME! 
     */
    public static final String toAsciiString(byte[] buffer, int startPos, 
                                             int length) {

        StringBuffer result = new StringBuffer();
        int endPoint = startPos + length;

        for (int i = startPos; i < endPoint; i++) {
            result.append(byteToChars[(int) buffer[i] - Byte.MIN_VALUE]);
        }

        return result.toString();
    }

}
