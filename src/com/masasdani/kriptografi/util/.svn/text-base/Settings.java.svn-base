package com.masasdani.kriptografi.util;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

public class Settings {
    
    public static byte[] key = null;
    
    public Settings() {
    }
    
    /**
     * Saves the current configuration of the application from the config.ini file
     */
    public static void saveConfiguration() {
        try {
            FileOutputStream f_out = new FileOutputStream("kripto.cfg");
            ObjectOutputStream obj_out = new ObjectOutputStream(f_out);
            if(key == null)
                obj_out.writeObject(new Boolean(false));
            else {
                obj_out.writeObject(new Boolean(true));
                obj_out.writeObject( Settings.key );
            }
            f_out.close();
        } catch (IOException ex) {
            ex.printStackTrace();
        }
    }
    
    /**
     * Loads the current configuration of the application from the config.ini file
     */
    public static void loadConfiguration() {
        if(new File("kripto.cfg").exists()) {
            try {
                FileInputStream f_in = new FileInputStream("kripto.cfg");
                ObjectInputStream obj_in = new ObjectInputStream(f_in);
                Boolean flag = (Boolean) obj_in.readObject();
                if(flag.booleanValue() == true) {
                    Settings.key = (byte[]) obj_in.readObject();
                }
                f_in.close();
            } catch (FileNotFoundException ex) {
                ex.printStackTrace();
            } catch (IOException ex) {
                ex.printStackTrace();
            } catch (ClassNotFoundException ex) {
                ex.printStackTrace();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
