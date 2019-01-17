/*
 * TCSS 305
 * Assignment 4 - Snapshop
 */

package gui;

import filters.EdgeDetectFilter;
import filters.EdgeHighlightFilter;
import filters.Filter;
import filters.FlipHorizontalFilter;
import filters.FlipVerticalFilter;
import filters.GrayscaleFilter;
import filters.SharpenFilter;
import filters.SoftenFilter;
import image.PixelImage;
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;




//import layouts.GridLayoutDemo;



/**
 * This is a simple SnapShopGUI app which is for editing the 
 * upload image with the filters.  
 * @author Arjun Prajapati
 * @version 3 November 2017
 */
public class SnapShopGUI extends JPanel {
    /** Default value. */
    private static final long serialVersionUID = 1L;
    
    /** The number of rows for filters. */
    private static final int ROW = 7;
    
    /** The number of rows for Window function button. */
    private static final int ROW1 = 3;
    
    /** The number of columns for buttons. */
    private static final int COL = 1;   
    
    /** Give default width for the JFrame. */
    private static final int WIDTH = 147;
    
    /** Give default width for the JFrame. */
    private static final int HEIGHT = 315;
    
    /** main window frame. */
    private JFrame myWindow;

    /** Panel for the filter buttons.  */
    private final JPanel myFilterBtnPanel;

    /** Panel for the myWindow function buttons. */
    private final JPanel myWindowBtnPanel;
   
    /** Reference value of PixelImage class. */
    private PixelImage myPixelImage;
    
    /** To store a choose file. */
    private final JFileChooser myFileChooser = new JFileChooser();
    
    /** To store directory of image.*/
    private final JLabel myImageLabel = new JLabel();
    
//    private final File myFile;
    /**
     * Panel for the All buttons.
     */
    private final JPanel myAllBtnPanel;
    

    /** List to store filter buttons. */
    private final java.util.List<JButton> myFilterButton;
    /** List to store filters. */
    private final java.util.List<Filter> myFilterList;
    
    /** Window function buttons Open. */
    private JButton myOpenBtn;
    /** Window function buttons Save. */
    private JButton mySaveBtn;
    /** Window function buttons Close. */
    private JButton myCloseBtn;
    /** JPanel for image.*/
    private JPanel myImagePanel;

    /**
     * Constructor to initialize the panels.
     */
    public SnapShopGUI() {
        super();
        myFilterBtnPanel = new JPanel(new GridLayout(ROW, COL));
        
        myWindowBtnPanel = new JPanel(new GridLayout(ROW1, COL));
        
        myFilterButton = new ArrayList<JButton>();
        
        myFilterList = new ArrayList<Filter>();
        
        myImagePanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        
        myAllBtnPanel = new JPanel(new BorderLayout());
       
        myOpenBtn = new JButton("Open...");
       
        mySaveBtn = new JButton("Save As...");
        
        myCloseBtn = new JButton("Close Image");

    }
    
    /**
     * This method is to make a filter buttons.
     */
    public void filterButtons() {
        
        filterButtons(new EdgeDetectFilter());
        filterButtons(new EdgeHighlightFilter());
        filterButtons(new FlipHorizontalFilter());
        filterButtons(new FlipVerticalFilter());
        filterButtons(new GrayscaleFilter());
        filterButtons(new SharpenFilter());
        filterButtons(new SoftenFilter());
    }
    /**
     * This method creates a buttons for filter and add action listener to them.
     * @param theFilter ,  instance of the Filter class.
     */
    public void filterButtons(final Filter theFilter) {
        // This line stores the Filter reference class to the list.
        myFilterList.add(theFilter);
        // This line gives a name to button with the respective function.
        final JButton filterBtnName = new JButton(theFilter.getDescription());
        // This line stores the Filter respective button to list.
        myFilterButton.add(filterBtnName);
        //THis line adds the action listener to the button.
        filterBtnName.addActionListener((ActionListener) new FilterBtnActionListener());
    }
    
        
    
    /**
     * Lay out the components and makes this frame visible.
     * This method is also for setting all the buttons.
     */
    public void setUpComponents() {
//        setLayout(new BorderLayout());
        
        filterButtons();
        // Loop for storing the filter button from list to the panel.
        for (int i = 0; i < myFilterButton.size(); i++) {
            myFilterBtnPanel.add(myFilterButton.get(i));
        }
        
        // The following codes are for the Window buttons adding to panel and action listener.
        add(myWindowBtnPanel, BorderLayout.SOUTH);
        myOpenBtn.addActionListener(new WindowButtonActionListener());
        mySaveBtn.addActionListener(new WindowButtonActionListener());
        myCloseBtn.addActionListener(new WindowButtonActionListener());
        myWindowBtnPanel.add(myOpenBtn);
        myWindowBtnPanel.add(mySaveBtn);
        myWindowBtnPanel.add(myCloseBtn);
        
        // Adding both filter and window button panel to window 
        // to it's with respective border direction.
        myAllBtnPanel.add(myFilterBtnPanel, BorderLayout.NORTH);
        myAllBtnPanel.add(myWindowBtnPanel, BorderLayout.SOUTH);
    }
    
    

    /**
     * This is the method which will be called from the main class. 
     */
    public void start() {
//       myFrame.setLayout(new BorderLayout());
        // Giving name to the frame.
        myWindow = new JFrame("TCSS 305 SnapShop");
        myWindow.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        setUpComponents();
        
        myWindow.add(myAllBtnPanel, BorderLayout.WEST);
        myWindow.add(myImagePanel, BorderLayout.CENTER);

        disableButton();

        myWindow.pack();
        myWindow.setMinimumSize(new Dimension(myWindow.getWidth(), myWindow.getHeight()));
        myWindow.setVisible(true);
       
       
    }
    
    /**
     * Default disable all button except open when image is not loaded.
     */
    public void disableButton() {
        for (int i = 0; i < myFilterButton.size(); i++) {
            myFilterButton.get(i).setEnabled(false);
        }
        mySaveBtn.setEnabled(false);
        myCloseBtn.setEnabled(false);

    }
    
    /**
     * Enable all buttons when image is loaded.
     */
    public void enableButton() {
        for (int i = 0; i < myFilterButton.size(); i++) {
            myFilterButton.get(i).setEnabled(true);
        }
        mySaveBtn.setEnabled(true);
        myCloseBtn.setEnabled(true);
    }
    
    /**
     * This is a inner class to perform the action of the filter button.
     * @author Arjun Prajapati
     * @version 3 November 2017
     *
     */
    public class FilterBtnActionListener implements ActionListener {
        
        @Override
        public void actionPerformed(final ActionEvent theEvent) {
            
            // This loop is to check which button is clicked, and do 
            //  the function with respect to the respective button task.
            for (int i = 0; i < myFilterButton.size(); i++) {
                if (theEvent.getSource().equals(myFilterButton.get(i))) {
                    myFilterList.get(i).filter(myPixelImage);
                    myImageLabel.setIcon(new ImageIcon(myPixelImage));
                    myWindow.pack();
                }
            }
            
        }
    }
    
    /**
     * This is an inner class for the action listener of myWindow buttons.
     * @author Arjun Prajapati
     * @version 3 November 2017
     */
    public class WindowButtonActionListener implements ActionListener {
        @Override
        public void actionPerformed(final ActionEvent theEvent) {
            /** Event for the Save As button. */
            if (theEvent.getSource() == mySaveBtn) {
                
                final int saveAction = myFileChooser.showSaveDialog(null);
                
                if (saveAction == JFileChooser.APPROVE_OPTION) {
                    
                    try {
                        myPixelImage.save(myFileChooser.getSelectedFile());
                        JOptionPane.showMessageDialog(null, "File Saved");
                   
                    } catch (final IOException e) {
                        JOptionPane.showMessageDialog(null, "Sorry, the file can't "
                                        + "be saved!", "File Save Error", 
                                        JOptionPane.ERROR_MESSAGE);
                    }
                    
                }
            }
            
            /** event for the Close Button. */
            if (theEvent.getSource() == myCloseBtn) {
                myImageLabel.setIcon(null);
//                myImagePanel.setPreferredSize(myImagePanelDimension);
                disableButton();
//                myImagePanel.setVisible(false);
//                myImagePanel.removeAll();
                
                myWindow.setMinimumSize(new Dimension(WIDTH, HEIGHT));
                myWindow.pack();

            }
            /** the action event for the myOpenBtn */
            if (theEvent.getSource() == myOpenBtn) {
                myFileChooser.setCurrentDirectory(new File("."));
                final int fileChoose = myFileChooser.showOpenDialog(null);
                if (fileChoose == JFileChooser.APPROVE_OPTION) {
            
                    final File imageFile = myFileChooser.getSelectedFile();
                    
                    try {
                        myPixelImage = PixelImage.load(imageFile);
                        myImageLabel.setIcon(new ImageIcon(myPixelImage));
            
                        myImagePanel.add(myImageLabel, BorderLayout.NORTH);
             
                        myWindow.setMinimumSize(new Dimension(0, 0));
                        myWindow.pack();
                        myWindow.setMinimumSize(new Dimension(myWindow.getWidth(),
                                                              myWindow.getHeight()));
            
                        enableButton();
            
                    } catch (final IOException e) {
                        JOptionPane.showMessageDialog(null, "The selected "
                                        + "file did not contain an image!",
                                                      "Error!", JOptionPane.ERROR_MESSAGE);
                    }
                }
            }
        }
    }
}
    

   
