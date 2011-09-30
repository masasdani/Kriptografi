/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package com.masasdani.kriptografi;

import com.masasdani.kriptografi.gui.MainFrame;
import com.masasdani.kriptografi.util.Settings;
import com.sun.java.swing.plaf.nimbus.NimbusLookAndFeel;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.UIManager;
import javax.swing.UnsupportedLookAndFeelException;

/**
 *
 * @author badak
 */
public class Main {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
        Settings.key="masasdani".getBytes();
        try{
            UIManager.setLookAndFeel(new NimbusLookAndFeel());
            java.awt.EventQueue.invokeLater(new Runnable() {
                public void run() {
                    MainFrame frame=new MainFrame();
                    frame.setLocationRelativeTo(null);
                    frame.setVisible(true);
                }
            });
        }catch(UnsupportedLookAndFeelException e){
            Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, e);
        }
    }
}
