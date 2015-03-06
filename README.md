# SimpleEncryption
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package examples;
import java.awt.Color;
import java.util.HashMap;


/**
 *
 * @author wctran
 */
public class CaesarGUI extends javax.swing.JFrame {
    private static final String alphabet = "abcdefghijklmnopqrstuvwxyz";
    private static final String decimal = "0123456789";
    private static final long serialVersionUID = 1L;    
       
    
    /**
     * Creates new form NewJFrame
     */
    public CaesarGUI() {
        initComponents();
    }

    
        
    public void encryptText(int selectedIndex) throws InterruptedException {
        //Get input text and put it all to lower-case so it's easy to convert
        String inputText = inputTA.getText().toLowerCase();
        String outputText = "";
        
        if(selectedIndex == 0){
            //Create a HashMap
            //A hash map takes keys and values, which are both Characters in this case.
            HashMap<Character, Character> alphaMap = new HashMap<Character, Character>();
            HashMap<Character, Character> decMap = new HashMap<Character, Character>();
            int shift;
            //Get the text from the app and store it in a String variable.
            String textNum = this.shiftFactor.getText();
            //Check to see if a "Shift Factor" value was entered.
            //If there wasn't, set shift to zero,
            //Otherwise parse the input value to an integer so we can use it.
            if(!textNum.equals("")){
                    shift = Integer.parseInt(textNum);
            }
            else{
                    shift = 0;
            }
            //Map every letter of the alphabet to another letter in the alphabet, shifted by x places.
            for(int i=0; i<alphabet.length(); i++){
                    alphaMap.put(alphabet.charAt(i), alphabet.charAt((i+shift)%26));
            } 
            for(int i=0; i<decimal.length(); i++){
                    decMap.put(decimal.charAt(i), decimal.charAt((i+shift)% 10));
            }  
            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(inputText.charAt(j) <= 122 && inputText.charAt(j)>= 97)    {
                    outputText = outputText.concat(alphaMap.get(inputText.charAt(j)).toString()); 
                } else if (inputText.charAt(j) <= 57 && inputText.charAt(j)>= 48) {
                    outputText = outputText.concat(decMap.get(inputText.charAt(j)).toString());
                } else {
                    outputText = outputText.concat(" ");
                }
            } 
            //Output the encrypted text
            outputTA.setText(outputText);        
            
        }
        
        else {
            int[] shift2 = new int [inputText.length()];
            
            if (selectedIndex == 1){
                shift2 = fibSeq(inputText.length()); 
            }
            else if(selectedIndex == 2){
                shift2 = cubeSeq(inputText.length());
            }
            else if(selectedIndex == 3){
                shift2 = triangularSeq(inputText.length());
            }
            
            
            /*
            if (selectedIndex == 2){
                shift2 = primeSeq(inputText.length()); 
            }*/
            
            
            
            StringBuilder sb = new StringBuilder();
            String str = inputText; 
            char[] charArray = str.toCharArray();
            
            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(charArray[j] >= 97 && charArray[j] <= 122){
                    charArray[j] = (char) (97 + ((charArray[j] - 97 + (shift2[j] % 26)) %26));
                }else if (charArray[j] >= 48 && charArray[j] <= 57){
                    charArray[j] = (char) (48 + (charArray[j] -48 + ( shift2[j] % 10))%10);
                } else {
                    charArray[j] = 32;
                }
                sb.append(charArray[j]);     
            }    
            outputText = sb.toString();
            outputTA.setText(outputText);
        }  
    }
    
    
    
    public void decryptText(int selectedIndex) throws InterruptedException{
         //Get input text and put it all to lower-case so it's easy to convert
        String inputText = outputTA.getText().toLowerCase();
        String outputText = "";
        
        if(selectedIndex == 0){
            //Create a HashMap
            HashMap<Character, Character> alphaMap = new HashMap<Character, Character>();
            HashMap<Character, Character> decMap = new HashMap<Character, Character>();
            int shift;
            String textNum = this.shiftFactor.getText();
            if(!textNum.equals("")){
                    shift = Integer.parseInt(textNum);
            }
            else{
                    shift = 0;
            }
            //Map every letter of the alphabet to another letter in the alphabet, shifted by x places.
            for(int i=0; i<alphabet.length(); i++){
                    alphaMap.put(alphabet.charAt(i), alphabet.charAt((i-shift%26+26)%26));
            } 
            for(int i=0; i<decimal.length(); i++){
                    decMap.put(decimal.charAt(i), decimal.charAt((i-shift%10+10)% 10));
            }  
            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(inputText.charAt(j) <= 122 && inputText.charAt(j)>= 97)    {
                    outputText = outputText.concat(alphaMap.get(inputText.charAt(j)).toString()); 
                } else if (inputText.charAt(j) <= 57 && inputText.charAt(j)>= 48) {
                    outputText = outputText.concat(decMap.get(inputText.charAt(j)).toString());
                } else {
                    outputText = outputText.concat(" ");
                }
            } 
            //Output the encrypted text
            inputTA.setText(outputText);        
            
        }
        
        else {
            int[] shift2 = new int [inputText.length()];
            
            if (selectedIndex == 1){
                shift2 = fibSeq(inputText.length()); 
            }
            else if(selectedIndex == 2){
                shift2 = cubeSeq(inputText.length());
            }
            else if(selectedIndex == 3){
                shift2 = triangularSeq(inputText.length());
            }  
            
            
            
            StringBuilder sb = new StringBuilder();
            String str = inputText; 
            char[] charArray = str.toCharArray();

            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(charArray[j] >= 97 && charArray[j] <= 122){
                    charArray[j] = (char) (97 + ((charArray[j] - 97 + (26 - shift2[j] % 26)) %26));
                }else if (charArray[j] >= 48 && charArray[j] <= 57){
                    charArray[j] = (char) (48 + (charArray[j] -48 + (10 - shift2[j] % 10))%10);
                } else {
                    charArray[j] = 32;
                }
                sb.append(charArray[j]);     
            }    
            outputText = sb.toString();
            inputTA.setText(outputText);
        }
    }
    
    
    
    public void decryptText2(int selectedIndex) throws InterruptedException{
         //Get input text and put it all to lower-case so it's easy to convert
        String inputText = inputTA.getText().toLowerCase();
        String outputText = "";
        
        if(selectedIndex == 0){
            //Create a HashMap
            HashMap<Character, Character> alphaMap = new HashMap<Character, Character>();
            HashMap<Character, Character> decMap = new HashMap<Character, Character>();
            int shift;
            String textNum = this.shiftFactor.getText();
            if(!textNum.equals("")){
                    shift = Integer.parseInt(textNum);
            }
            else{
                    shift = 0;
            }
            //Map every letter of the alphabet to another letter in the alphabet, shifted by x places.
            for(int i=0; i<alphabet.length(); i++){
                    alphaMap.put(alphabet.charAt(i), alphabet.charAt((i-shift%26+26)%26));
            } 
            for(int i=0; i<decimal.length(); i++){
                    decMap.put(decimal.charAt(i), decimal.charAt((i-shift%10+10)% 10));
            }  
            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(inputText.charAt(j) <= 122 && inputText.charAt(j)>= 97)    {
                    outputText = outputText.concat(alphaMap.get(inputText.charAt(j)).toString()); 
                } else if (inputText.charAt(j) <= 57 && inputText.charAt(j)>= 48) {
                    outputText = outputText.concat(decMap.get(inputText.charAt(j)).toString());
                } else {
                    outputText = outputText.concat(" ");
                }
            } 
            //Output the encrypted text
            outputTA.setText(outputText);        
            
        }
        
        else {
            int[] shift2 = new int [inputText.length()];
            
            if (selectedIndex == 1){
                shift2 = fibSeq(inputText.length()); 
            }
            else if(selectedIndex == 2){
                shift2 = cubeSeq(inputText.length());
            }
            else if(selectedIndex == 3){
                shift2 = triangularSeq(inputText.length());
            }
            
            
            StringBuilder sb = new StringBuilder();
            String str = inputText; 
            char[] charArray = str.toCharArray();

            //Go to each letter and switch it with it's shifted counterpart
            for(int j=0; j<inputText.length(); j++){
                if(charArray[j] >= 97 && charArray[j] <= 122){
                    charArray[j] = (char) (97 + ((charArray[j] - 97 + (26 - shift2[j] % 26)) %26));
                }else if (charArray[j] >= 48 && charArray[j] <= 57){
                    charArray[j] = (char) (48 + (charArray[j] -48 + (10 - shift2[j] % 10))%10);
                } else {
                    charArray[j] = 32;
                }
                sb.append(charArray[j]);     
            }    
            outputText = sb.toString();
            outputTA.setText(outputText);
        }
    }
        
  
    
    
    
    //Fibonacci sequence
    private int[] fibSeq(int length){
        int[] fibonacci = new int[length];
        for(int i = 0; i < fibonacci.length; i++){
            if(i == 0 || i == 1){
                fibonacci[i] = i;
            } else {
                fibonacci[i] = fibonacci[i-1]+fibonacci[i-2]    ;       
            }
        }
        return fibonacci;
    }
    
    
    
    
    
    //Factorial sequence
    private int[] facSeq(int length){
        int[] sequence = new int[length];
        for(int i = 0; i < sequence.length; i++){
            if(i==0 || i == 1){
                sequence[i] = 1;
            } else {                
                sequence[i] = i * sequence[i-1];
            }    
        }
        return sequence ;
    }
    
    private int[] cubeSeq(int length){
        int[] sequence = new int[length];
        for(int i = 0; i < sequence.length; i++){
            sequence[i] = i * i * i;
        }
        return sequence ;
    }
    
    private int[] triangularSeq(int length){
        int[] sequence = new int[length];
        for(int i = 0; i < sequence.length; i++){
            sequence[i] = i * (i + 1) / 2;
        }
        return sequence ;
    }
    
    
    /*
    private int[] primeSeq(int length){
        int[] sequence = new int[length];
        for(int i = 0; i < sequence.length; i++){
            //ADDCODE
    
        }
        return sequence ;
    }
    */
    
    
    
    
    
    //  NEW SEQUENCE (TEMPLATE)

    
    
    
    
    
    
    
    
    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        shiftFactor = new javax.swing.JTextField();
        shiftSelect = new javax.swing.JComboBox();
        decryptButton2 = new javax.swing.JButton();
        decryptButton = new javax.swing.JButton();
        encryptButton = new javax.swing.JButton();
        inputTA = new javax.swing.JTextArea();
        outputTA = new javax.swing.JTextArea();
        background = new javax.swing.JPanel();
        shiftTypeLabel = new javax.swing.JLabel();
        shiftFactorLabel = new javax.swing.JLabel();
        Title = new javax.swing.JLabel();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        setLocationByPlatform(true);
        setPreferredSize(new java.awt.Dimension(420, 260));
        setResizable(false);
        getContentPane().setLayout(null);

        shiftFactor.setBackground(java.awt.Color.black);
        shiftFactor.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        shiftFactor.setForeground(java.awt.Color.yellow);
        getContentPane().add(shiftFactor);
        shiftFactor.setBounds(300, 220, 75, 25);

        shiftSelect.setBackground(java.awt.Color.black);
        shiftSelect.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        shiftSelect.setForeground(java.awt.Color.green);
        shiftSelect.setModel(new javax.swing.DefaultComboBoxModel(new String[] { "Normal", "Fibonacci", "Cube", "Triangular" }));
        shiftSelect.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                shiftSelectActionPerformed(evt);
            }
        });
        getContentPane().add(shiftSelect);
        shiftSelect.setBounds(100, 220, 105, 25);

        decryptButton2.setBackground(java.awt.Color.red);
        decryptButton2.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        decryptButton2.setText("Decrypt");
        decryptButton2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                decryptButton2ActionPerformed(evt);
            }
        });
        getContentPane().add(decryptButton2);
        decryptButton2.setBounds(287, 171, 80, 27);

        decryptButton.setBackground(java.awt.Color.red);
        decryptButton.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        decryptButton.setText("Decrypt");
        decryptButton.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                decryptButtonActionPerformed(evt);
            }
        });
        getContentPane().add(decryptButton);
        decryptButton.setBounds(287, 86, 80, 27);

        encryptButton.setBackground(java.awt.Color.green);
        encryptButton.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        encryptButton.setText("Encrypt");
        encryptButton.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                encryptButtonActionPerformed(evt);
            }
        });
        getContentPane().add(encryptButton);
        encryptButton.setBounds(287, 47, 80, 27);

        inputTA.setBackground(java.awt.Color.black);
        inputTA.setColumns(20);
        inputTA.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        inputTA.setForeground(java.awt.Color.yellow);
        inputTA.setLineWrap(true);
        inputTA.setRows(5);
        getContentPane().add(inputTA);
        inputTA.setBounds(40, 40, 140, 75);

        outputTA.setBackground(java.awt.Color.black);
        outputTA.setColumns(20);
        outputTA.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        outputTA.setForeground(java.awt.Color.yellow);
        outputTA.setLineWrap(true);
        outputTA.setRows(5);
        getContentPane().add(outputTA);
        outputTA.setBounds(40, 130, 140, 75);

        background.setBackground(java.awt.Color.black);

        shiftTypeLabel.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        shiftTypeLabel.setForeground(java.awt.Color.green);
        shiftTypeLabel.setText("Shift Type");

        shiftFactorLabel.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        shiftFactorLabel.setForeground(java.awt.Color.green);
        shiftFactorLabel.setText("Shift Factor");

        Title.setFont(new java.awt.Font("Monospaced", 0, 12)); // NOI18N
        Title.setForeground(java.awt.Color.green);
        Title.setText("Caesar Encryption - (a to z, 0 to 9, else set to null)");

        javax.swing.GroupLayout backgroundLayout = new javax.swing.GroupLayout(background);
        background.setLayout(backgroundLayout);
        backgroundLayout.setHorizontalGroup(
            backgroundLayout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(backgroundLayout.createSequentialGroup()
                .addGap(23, 23, 23)
                .addGroup(backgroundLayout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(Title)
                    .addGroup(backgroundLayout.createSequentialGroup()
                        .addComponent(shiftTypeLabel)
                        .addGap(118, 118, 118)
                        .addComponent(shiftFactorLabel)))
                .addContainerGap(19, Short.MAX_VALUE))
        );
        backgroundLayout.setVerticalGroup(
            backgroundLayout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, backgroundLayout.createSequentialGroup()
                .addContainerGap()
                .addComponent(Title)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 198, Short.MAX_VALUE)
                .addGroup(backgroundLayout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(shiftTypeLabel)
                    .addComponent(shiftFactorLabel))
                .addGap(40, 40, 40))
        );

        getContentPane().add(background);
        background.setBounds(0, 0, 420, 280);

        pack();
    }// </editor-fold>                        

    private void encryptButtonActionPerformed(java.awt.event.ActionEvent evt) {                                              
                try{
                        encryptText(shiftSelect.getSelectedIndex());
                } catch(InterruptedException e1){
                        e1.printStackTrace();
                }
    }                                             

    private void decryptButton2ActionPerformed(java.awt.event.ActionEvent evt) {                                               
                try {
                    decryptText(shiftSelect.getSelectedIndex());
                 } catch (InterruptedException e1) {
                    e1.printStackTrace();
                }
    }                                              

    private void decryptButtonActionPerformed(java.awt.event.ActionEvent evt) {                                              
                try {
                    decryptText2(shiftSelect.getSelectedIndex());
                } catch (InterruptedException e1) {
                    e1.printStackTrace();
                }
    }                                             

    private void shiftSelectActionPerformed(java.awt.event.ActionEvent evt) {                                            
        if(shiftSelect.getSelectedIndex() != 0){
            shiftFactor.enable(false);
            shiftFactor.setBackground(Color.darkGray);
            shiftFactor.setOpaque(false);
        } else {
            shiftFactor.enable(true);
            shiftFactor.setBackground(Color.BLACK);
            shiftFactor.setOpaque(true);
        }
    }                                           
       
    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(CaesarGUI.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(CaesarGUI.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(CaesarGUI.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(CaesarGUI.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new CaesarGUI().setVisible(true);
            }
        });
    }

    
    
    // Variables declaration - do not modify                     
    private javax.swing.JLabel Title;
    private javax.swing.JPanel background;
    private javax.swing.JButton decryptButton;
    private javax.swing.JButton decryptButton2;
    private javax.swing.JButton encryptButton;
    private javax.swing.JTextArea inputTA;
    private javax.swing.JTextArea outputTA;
    private javax.swing.JTextField shiftFactor;
    private javax.swing.JLabel shiftFactorLabel;
    private javax.swing.JComboBox shiftSelect;
    private javax.swing.JLabel shiftTypeLabel;
    // End of variables declaration                   
}
