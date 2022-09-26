# TaxFyle

This program helps you calculate income tax!
Takes in an input of w-2 wages earned & uses a HashMap to calculate the income taxes depending on one of the 50 states that the user picks. 

package program;



import java.io.FileWriter;
import java.io.IOException;
import java.util.Formatter;
import java.util.HashMap;
import javax.swing.JOptionPane;

/**
 *
 * @author chris
 */
public class Home extends javax.swing.JFrame {

    /**
     * Creates new form Home
     */
    public Home() {
        initComponents();
        taxRates = new HashMap<>();
        taxRates.put("Illinois", 0.0495);
        taxRates.put("Utah", 0.0495);
        taxRates.put("Massachusetts", 0.05);
        taxRates.put("Kentucky", 0.0500);
        taxRates.put("Pennsylvania", 0.0307);
        taxRates.put("Colorado", 0.0455);
        taxRates.put("Indiana", 0.0323);
        taxRates.put("Washington", 0.07);
        taxRates.put("Michigan", 0.0425);
        taxRates.put("Texas", 0.00);
        taxRates.put("Nevada", 0.00);
        taxRates.put("North Carolina", 0.0499);
        taxRates.put("South Dakota", 0.00);
        taxRates.put("Florida", 0.00);
        taxRates.put("New Hampshire", 0.00); // 0.05 interest and dividents AKA only based on stock market
        taxRates.put("Wyoming", 0.00);
        taxRates.put("Tennessee", 0.00);
        taxRates.put("Alaska", 0.00);
        
        complexTaxRates = new HashMap<>();
        
        complexTaxRates.put("Alabama", new Double[][]{{0.02,0.04,0.05}, {0.0,500.0,3000.0}});
        complexTaxRates.put("California", new Double [][] {{0.01, 0.02, 0.04, 0.06, 0.08, 0.093, 0.103, 0.113, 0.123, 0.133}, 
            {0.0, 9325.0, 22107.0, 34892.0, 
            48435.0, 61214.0, 312686.0, 375221.0, 625369.0, 100000000.0}});
        complexTaxRates.put("Arizona", new Double [][] {{0.0259, 0.0334, 0.0417, 0.0450}, {0.0, 27808.0, 55615.0, 166843.0}});
        complexTaxRates.put("Arkansas", new Double [][] {{0.020, 0.04, 0.0550}, {0.0, 4300.0, 8500.0}});
        complexTaxRates.put("Connecticut", new Double [][] {{0.300, 0.05, 0.055, 0.060, 0.065, 0.069, 0.0699}, {0.0, 10000.0, 50000.0, 
            100000.0, 200000.0, 250000.0, 500000.0}});
        complexTaxRates.put("Delaware", new Double [][] {{0.0220, 0.0480, 0.0520, 0.055, 0.0660}, {2000.0, 5000.0, 10000.0, 20000.0, 
            25000.0, 60000.0}});
        complexTaxRates.put("Georgia", new Double [][] {{0.01, 0.02, 0.03, 0.04, 0.05, 0.0575}, {0.0, 750.0, 2250.0, 3750.0, 5250.0, 
            7000.0}});
        complexTaxRates.put("Hawaii", new Double [][] {{0.0140, 0.0320, 0.0550, 0.0640, 0.0680, 0.0720, 0.0760, 0.0790, 0.0825, 0.09,
            0.10, 0.11}, {0.0, 2400.0, 4800.0, 9600.0, 14400.0, 
        19200.0, 24000.0, 36000.0, 48000.0, 150000.0, 175000.0, 200000.0}});
        complexTaxRates.put("Idaho", new Double [][] {{0.01, 0.03, 0.045, 0.06}, {0.0, 1588.0, 4763.0, 7939.0}});
        complexTaxRates.put("Iowa", new Double [][] {{0.0033, 0.0067, 0.025, 0.0414, 0.0563, 0.0596, 0.0625, 0.0744, 0.0853}, {0.0, 
            1743.0, 3486.0, 6972.0, 15687.0, 26145.0, 34860.0, 52290.0,
        78435.0}});
        complexTaxRates.put("Kansas", new Double [][] {{0.0310, 0.0525, 0.0570}, {0.0, 15000.0, 30000.0}});
        complexTaxRates.put("Louisiana", new Double [][] {{0.0185, 0.0350, 0.0425}, {0.0, 12500.0, 50000.0}});
        complexTaxRates.put("Maine", new Double[][]{{0.0580, 0.0675, 0.0715}, {0.0, 23000.0, 54450.0}});
        complexTaxRates.put("Maryland", new Double[][]{{0.02, 0.03, 0.04, 0.0475, 0.05, 0.0525, 0.055, 0.0575}, {0.0, 1000.0, 2000.0, 
            3000.0, 100000.0, 125000.0, 150000.0, 250000.0}});
        complexTaxRates.put("Minnesota", new Double[][]{{0.0535, 0.0680, 0.0785, 0.0985}, {0.0, 28080.0, 92230.0, 171220.0}});
        complexTaxRates.put("Mississippi", new Double[][]{{0.04, 0.05}, {5000.0, 10000.0}});
        complexTaxRates.put("Missouri", new Double[][]{{0.0150, 0.02, 0.025, 0.03, 0.035, 0.04, 0.045, 0.05, 0.054}, {108.0, 1088.0,
            2176.0, 3264.0, 4352.0, 5440.0, 6528.0, 7616.0, 8704.0}});
        complexTaxRates.put("Montana", new Double[][]{{0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 0.0675}, {0.0, 3100.0, 5500.0, 8400.0, 
            11400.0, 14600.0, 18800.0}});
        complexTaxRates.put("Nebraska", new Double[][]{{0.0246, 0.0351, 0.0501, 0.0684}, {0.0, 3440.0, 20590.0, 33180.0}});
        complexTaxRates.put("New Jersey", new Double[][]{{0.014, 0.01750, 0.0350, 0.0525, 0.0637, 0.0897, 0.10750}, {0.0, 20000.0, 
            35000.0, 40000.0, 75000.0, 500000.0, 100000000.0}});
        complexTaxRates.put("New Mexico", new Double[][]{{0.017, 0.0320, 0.0470, 0.0490, 0.0590}, {0.0, 5500.0, 11000.0, 16000.0, 
            210000.0}});
        complexTaxRates.put("New York", new Double[][]{{0.04, 0.0450, 0.0525, 0.0585, 0.0625, 0.0685, 0.0965, 0.1030, 0.1090}, {0.0, 
            8500.0, 11700.0, 13900.0, 80650.0, 215400.0, 1077550.0, 
        5000000.0, 25000000.0}});
        complexTaxRates.put("North Dakota", new Double[][]{{0.010, 0.0204, 0.027, 0.0264, 0.029}, {0.0, 40525.0, 98100.0, 204675.0, 
            445000.0}});
        complexTaxRates.put("Ohio", new Double[][]{{0.0275, 0.03226, 0.03688, 0.03990}, {25000.0, 44250.0, 88450.0, 110650.0}});
        complexTaxRates.put("Oklahoma", new Double[][]{{0.0025, 0.0075, 0.0175, 0.0275, 0.0375, 0.0475}, {0.0, 1000.0, 2500.0, 3750.0, 
            4900.0, 7200.0}});
        complexTaxRates.put("Oregon", new Double[][]{{0.045, 0.0675, 0.0875, 0.0909}, {0.0, 3650.0, 9200.0, 1250000.0}});
        complexTaxRates.put("Rhode Island", new Double[][]{{0.0375, 0.0475, 0.0599}, {0.0, 68200.0, 155050.0}});
        complexTaxRates.put("South Carolina", new Double[][]{{0.00, 0.03, 0.04, 0.05, 0.06, 0.07}, {0.0, 3200.0, 6410.0, 9620.0, 
            12820.0, 16040.0}});
        complexTaxRates.put("Vermont", new Double[][]{{0.035, 0.0660, 0.0760,0.08750}, {0.0, 40950.0, 99200.0, 206950.0}});
        complexTaxRates.put("Virginia", new Double[][]{{0.02, 0.03, 0.05, 0.0575}, {0.0, 3000.0, 5000.0, 17000.0}});
        complexTaxRates.put("West Virginia", new Double[][]{{0.0300, 0.04, 0.045, 0.06, 0.065}, {0.0, 10000.0, 25000.0, 40000.0, 
            60000.0}});
        complexTaxRates.put("Wisconsin", new Double[][]{{0.0354, 0.0465, 0.0530, 0.0765}, {0.0, 12760.0, 25520.0, 280950.0}});
    }
    
   
    
    HashMap<String, Double> taxRates;
    HashMap<String, Double [] [] > complexTaxRates;
    
    public void updateTotaltax(){
        try{
      if(Integer.parseInt(wagesEarned.getText()) < 0){
           JOptionPane.showMessageDialog(this, "Please Enter Positive Wages");   
       }
      else{
       String rawText = wagesEarned.getText();
   
            double input = Double.parseDouble(rawText);
            String state = stateBox.getSelectedItem().toString();
            double output = 0.0;
            if(taxRates.containsKey(state)){
                 double rate = taxRates.get(state);
                 output = rate * input;
            }
            else{
                boolean salaryFlag = true;
                Double values [][] = complexTaxRates.get(state);
                // iterating through the array... takes first array (interest rates) * the min of upperbound second array (salary) && the inputted wage 
                //(Math.min compares second array, input) - lowerbound (tax only in between)
                for(int i = 0; i < values[1].length - 1; i++){
                  output +=  values[0][i] * (Math.min(values[1][i+1], input) - values[1][i]);
                  if(input < values[1][i + 1]){
                      salaryFlag = false;
                      break;
                  } 
                }
                //if salary is above heighest tax bracket, then salary - highest tax bracket times highest tax rate. 
                //last index gives last number (last salary)
                //ie. salary = 5000, state = Alabama, $3000+ -- 0.05 tax rate . (5000 - 3000) * 0.05 (percent).
                if(salaryFlag){
                int lastIndex = values[1].length - 1;
                output += (input - values [1][lastIndex]) * values [0][lastIndex];
            }
            }
            //formats
            StringBuilder builder = new StringBuilder();
            Formatter format = new Formatter(builder);
            format.format("%.2f", output);
            taxesOutput.setText("$ " + builder.toString());
    }
    }
                 catch(NumberFormatException e){
           JOptionPane.showMessageDialog(this, "Please Enter a valid Wage");   
         }
    }
    
    

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        buttonGroup1 = new javax.swing.ButtonGroup();
        jTextField2 = new javax.swing.JTextField();
        jLabel1 = new javax.swing.JLabel();
        jPanel1 = new javax.swing.JPanel();
        jLabel3 = new javax.swing.JLabel();
        jLabel6 = new javax.swing.JLabel();
        jLabel5 = new javax.swing.JLabel();
        jLabel2 = new javax.swing.JLabel();
        jLabel7 = new javax.swing.JLabel();
        jLabel9 = new javax.swing.JLabel();
        jLabel10 = new javax.swing.JLabel();
        jLabel11 = new javax.swing.JLabel();
        jLabel8 = new javax.swing.JLabel();
        jPanel2 = new javax.swing.JPanel();
        jLabel4 = new javax.swing.JLabel();
        jLabel12 = new javax.swing.JLabel();
        jLabel13 = new javax.swing.JLabel();
        jLabel14 = new javax.swing.JLabel();
        jLabel15 = new javax.swing.JLabel();
        firstName = new javax.swing.JTextField();
        lastName = new javax.swing.JTextField();
        date = new javax.swing.JTextField();
        wagesEarned = new javax.swing.JTextField();
        jLabel16 = new javax.swing.JLabel();
        Save = new javax.swing.JButton();
        stateBox = new javax.swing.JComboBox<>();
        jLabel17 = new javax.swing.JLabel();
        jTextField6 = new javax.swing.JTextField();
        jLabel18 = new javax.swing.JLabel();
        taxesOutput = new javax.swing.JTextField();
        calculate = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        setAlwaysOnTop(true);
        setBackground(new java.awt.Color(255, 255, 255));
        getContentPane().setLayout(new org.netbeans.lib.awtextra.AbsoluteLayout());
        getContentPane().add(jLabel1, new org.netbeans.lib.awtextra.AbsoluteConstraints(1165, 1, 37, -1));

        jPanel1.setBackground(new java.awt.Color(51, 153, 255));

        jLabel3.setFont(new java.awt.Font("Franklin Gothic Book", 1, 60)); // NOI18N
        jLabel3.setForeground(new java.awt.Color(255, 255, 255));
        jLabel3.setText("Taxfyle");

        jLabel6.setIcon(new javax.swing.ImageIcon(getClass().getResource("/program/taxes.png"))); // NOI18N

        jLabel5.setFont(new java.awt.Font("Brush Script MT", 1, 24)); // NOI18N
        jLabel5.setForeground(new java.awt.Color(255, 255, 255));
        jLabel5.setText("Est. 2015");

        jLabel2.setFont(new java.awt.Font("Comic Sans MS", 1, 24)); // NOI18N
        jLabel2.setForeground(new java.awt.Color(255, 255, 255));
        jLabel2.setText("\"Your Taxes Made Easy\"");

        jLabel7.setFont(new java.awt.Font("Comic Sans MS", 1, 18)); // NOI18N
        jLabel7.setForeground(new java.awt.Color(255, 255, 255));
        jLabel7.setHorizontalAlignment(javax.swing.SwingConstants.TRAILING);
        jLabel7.setText("2901 Florida Ave ste 840 Miami, Fl");

        jLabel9.setFont(new java.awt.Font("Comic Sans MS", 1, 18)); // NOI18N
        jLabel9.setForeground(new java.awt.Color(255, 255, 255));
        jLabel9.setText("Call TODAY for more information!");

        jLabel10.setIcon(new javax.swing.ImageIcon(getClass().getResource("/program/map.png"))); // NOI18N

        jLabel11.setIcon(new javax.swing.ImageIcon(getClass().getResource("/program/arrow-right.png"))); // NOI18N

        jLabel8.setFont(new java.awt.Font("Comic Sans MS", 1, 24)); // NOI18N
        jLabel8.setForeground(new java.awt.Color(255, 255, 255));
        jLabel8.setText("(888) - 803 - 4458");

        jPanel2.setBackground(new java.awt.Color(255, 255, 255));

        jLabel4.setIcon(new javax.swing.ImageIcon(getClass().getResource("/program/1569513731037.jpg"))); // NOI18N

        jLabel12.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel12.setText("Client First Name:");

        jLabel13.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel13.setText("Client Last Name:");

        jLabel14.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel14.setText("Date: (MM/DD/YY):");

        jLabel15.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel15.setText("Wages Earned W-2: ");

        firstName.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                firstNameActionPerformed(evt);
            }
        });

        date.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                dateActionPerformed(evt);
            }
        });

        wagesEarned.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                wagesEarnedActionPerformed(evt);
            }
        });
        wagesEarned.addKeyListener(new java.awt.event.KeyAdapter() {
            public void keyPressed(java.awt.event.KeyEvent evt) {
                wagesEarnedKeyPressed(evt);
            }
        });

        jLabel16.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel16.setText("Total Taxes That Needs To be Paid:");

        Save.setFont(new java.awt.Font("Comic Sans MS", 1, 36)); // NOI18N
        Save.setForeground(new java.awt.Color(0, 204, 255));
        Save.setText("Save");
        Save.setBorder(new javax.swing.border.SoftBevelBorder(javax.swing.border.BevelBorder.RAISED, new java.awt.Color(51, 0, 255), new java.awt.Color(51, 0, 255), new java.awt.Color(51, 0, 255), new java.awt.Color(51, 0, 255)));
        Save.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                SaveActionPerformed(evt);
            }
        });

        stateBox.setModel(new javax.swing.DefaultComboBoxModel<>(new String[] { "Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware", "Florida", "Georgia", "Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky", "Louisiana", "Maine", "Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi", "Missouri", "Montana", "Nebraska", "Nevada", "New Hampshire", "New Jersey", "New Mexico", "New York", "North Carolina", "North Dakota", "Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island", "South Carolina", "South Dakota", "Tennessee", "Texas", "Utah", "Vermont", "Virginia", "Washington", "West Virginia", "Wisconsin", "Wyoming" }));
        stateBox.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                stateBoxActionPerformed(evt);
            }
        });

        jLabel17.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jLabel17.setText("State:");

        jTextField6.setFont(new java.awt.Font("Comic Sans MS", 0, 18)); // NOI18N
        jTextField6.setForeground(new java.awt.Color(255, 204, 0));
        jTextField6.setText("Program accounts for Single File Tax  by State ");
        jTextField6.setBorder(null);
        jTextField6.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jTextField6ActionPerformed(evt);
            }
        });

        jLabel18.setIcon(new javax.swing.ImageIcon(getClass().getResource("/program/star.png"))); // NOI18N

        calculate.setFont(new java.awt.Font("Comic Sans MS", 1, 14)); // NOI18N
        calculate.setForeground(new java.awt.Color(0, 204, 255));
        calculate.setText("Calculate");
        calculate.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                calculateActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
        jPanel2.setLayout(jPanel2Layout);
        jPanel2Layout.setHorizontalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, jPanel2Layout.createSequentialGroup()
                .addGap(0, 0, Short.MAX_VALUE)
                .addComponent(jLabel4, javax.swing.GroupLayout.PREFERRED_SIZE, 188, javax.swing.GroupLayout.PREFERRED_SIZE))
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addGap(86, 86, 86)
                .addComponent(jLabel16, javax.swing.GroupLayout.PREFERRED_SIZE, 421, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jLabel18, javax.swing.GroupLayout.PREFERRED_SIZE, 24, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(11, 11, 11)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(jTextField6, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 166, Short.MAX_VALUE)
                        .addComponent(Save)
                        .addGap(15, 15, 15))
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel12, javax.swing.GroupLayout.PREFERRED_SIZE, 161, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel13, javax.swing.GroupLayout.PREFERRED_SIZE, 161, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel14, javax.swing.GroupLayout.PREFERRED_SIZE, 187, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel15, javax.swing.GroupLayout.PREFERRED_SIZE, 187, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel17, javax.swing.GroupLayout.PREFERRED_SIZE, 187, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGap(36, 36, 36)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(stateBox, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                .addComponent(firstName, javax.swing.GroupLayout.PREFERRED_SIZE, 254, javax.swing.GroupLayout.PREFERRED_SIZE)
                                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                                    .addComponent(lastName)
                                    .addComponent(date)
                                    .addComponent(wagesEarned, javax.swing.GroupLayout.DEFAULT_SIZE, 254, Short.MAX_VALUE))))
                        .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))))
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, jPanel2Layout.createSequentialGroup()
                .addGap(18, 18, 18)
                .addComponent(calculate, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addComponent(taxesOutput, javax.swing.GroupLayout.PREFERRED_SIZE, 455, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(103, 103, 103))
        );
        jPanel2Layout.setVerticalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, jPanel2Layout.createSequentialGroup()
                .addComponent(jLabel4, javax.swing.GroupLayout.PREFERRED_SIZE, 135, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jLabel12)
                    .addComponent(firstName, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(14, 14, 14)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jLabel13)
                    .addComponent(lastName, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(18, 18, 18)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jLabel14)
                    .addComponent(date, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(29, 29, 29)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(stateBox, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel17))
                .addGap(29, 29, 29)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jLabel15)
                    .addComponent(wagesEarned, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 92, Short.MAX_VALUE)
                .addComponent(jLabel16)
                .addGap(18, 18, 18)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(taxesOutput, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(calculate))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addGap(79, 79, 79)
                        .addComponent(jTextField6, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, jPanel2Layout.createSequentialGroup()
                        .addGap(48, 48, 48)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                            .addComponent(Save)
                            .addComponent(jLabel18, javax.swing.GroupLayout.PREFERRED_SIZE, 21, javax.swing.GroupLayout.PREFERRED_SIZE))))
                .addGap(19, 19, 19))
        );

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jLabel10)
                        .addGap(19, 19, 19)
                        .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(jPanel1Layout.createSequentialGroup()
                                .addComponent(jLabel11, javax.swing.GroupLayout.PREFERRED_SIZE, 40, javax.swing.GroupLayout.PREFERRED_SIZE)
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                                .addComponent(jLabel8))
                            .addComponent(jLabel7)))
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(38, 38, 38)
                        .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel9, javax.swing.GroupLayout.PREFERRED_SIZE, 338, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel2, javax.swing.GroupLayout.PREFERRED_SIZE, 338, javax.swing.GroupLayout.PREFERRED_SIZE)))
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(18, 18, 18)
                        .addComponent(jLabel6, javax.swing.GroupLayout.PREFERRED_SIZE, 82, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(jLabel3, javax.swing.GroupLayout.PREFERRED_SIZE, 263, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(120, 120, 120)
                        .addComponent(jLabel5, javax.swing.GroupLayout.PREFERRED_SIZE, 139, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addGap(18, 18, 18)
                .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(0, 0, Short.MAX_VALUE))
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addGap(28, 28, 28)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jLabel3)
                    .addComponent(jLabel6))
                .addGap(40, 40, 40)
                .addComponent(jLabel2)
                .addGap(70, 70, 70)
                .addComponent(jLabel9)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                    .addComponent(jLabel11, javax.swing.GroupLayout.PREFERRED_SIZE, 52, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel8))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jLabel7)
                    .addComponent(jLabel10, javax.swing.GroupLayout.PREFERRED_SIZE, 24, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(39, 39, 39)
                .addComponent(jLabel5)
                .addGap(66, 66, 66))
            .addComponent(jPanel2, javax.swing.GroupLayout.Alignment.TRAILING, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
        );

        getContentPane().add(jPanel1, new org.netbeans.lib.awtextra.AbsoluteConstraints(6, 0, -1, -1));

        pack();
    }// </editor-fold>                        

    private void stateBoxActionPerformed(java.awt.event.ActionEvent evt) {                                         
       // updateTotaltax();      
    }                                        

    private void wagesEarnedActionPerformed(java.awt.event.ActionEvent evt) {                                            

    }                                           

    private void SaveActionPerformed(java.awt.event.ActionEvent evt) {                                     
      boolean invalidInput = false;   
      if(firstName.getText().trim().isEmpty()){
           JOptionPane.showMessageDialog(this, "Please Fill Out first name box");
           invalidInput = true;
      }
       if(lastName.getText().trim().isEmpty()){
           JOptionPane.showMessageDialog(this, "Please Fill Out last name box");
           invalidInput = true;
      }
       if(date.getText().trim().isEmpty()){
           JOptionPane.showMessageDialog(this, "Please Fill Date Field");
           invalidInput = true;
      }
       if(wagesEarned.getText().trim().isEmpty()){
         JOptionPane.showMessageDialog(this, "Please Enter Wages Earned");   
         invalidInput = true;
      }
     
       if(!invalidInput){
        try{
            updateTotaltax();
            FileWriter writer = new FileWriter("data.txt");
            writer.write("First Name: " + firstName.getText() + "\n" + "Last name: " + lastName.getText() +
                    "\n" + "Date: " + date.getText() + "\n" + "State: " + stateBox.getSelectedItem().toString() + "\n" + "Wages Earned: " 
                    + wagesEarned.getText() + "\n" + "Amount need to be paid: " + taxesOutput.getText());
            
            writer.close();
            JOptionPane.showMessageDialog(this, "Client successfully saved in data.txt file");   
            System.exit(0);
        }
        catch(IOException e){
            e.printStackTrace();
        }
      }
    }                                    
      
    private void firstNameActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
    }                                         

    private void jTextField6ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        // TODO add your handling code here:
    }                                           

    private void dateActionPerformed(java.awt.event.ActionEvent evt) {                                     
        // TODO add your handling code here:
    }                                    

    private void calculateActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        updateTotaltax();
    }                                         

    private void wagesEarnedKeyPressed(java.awt.event.KeyEvent evt) {                                       
      
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
            java.util.logging.Logger.getLogger(Home.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(Home.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(Home.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(Home.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new Home().setVisible(true);
            }
        });

    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton Save;
    private javax.swing.ButtonGroup buttonGroup1;
    private javax.swing.JButton calculate;
    private javax.swing.JTextField date;
    private javax.swing.JTextField firstName;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel13;
    private javax.swing.JLabel jLabel14;
    private javax.swing.JLabel jLabel15;
    private javax.swing.JLabel jLabel16;
    private javax.swing.JLabel jLabel17;
    private javax.swing.JLabel jLabel18;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JLabel jLabel6;
    private javax.swing.JLabel jLabel7;
    private javax.swing.JLabel jLabel8;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JTextField jTextField2;
    private javax.swing.JTextField jTextField6;
    private javax.swing.JTextField lastName;
    private javax.swing.JComboBox<String> stateBox;
    private javax.swing.JTextField taxesOutput;
    private javax.swing.JTextField wagesEarned;
    // End of variables declaration                   
}

