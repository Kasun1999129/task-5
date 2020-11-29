# task-5

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.util.Vector;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.table.DefaultTableModel;
        

public class Employee extends javax.swing.JFrame {

    public Employee() {
        initComponents();
    }
  	private void tableMouseClicked(java.awt.event.MouseEvent evt) {                                    
        // TODO add your handling code here:
        DefaultTableModel Df=(DefaultTableModel)table5.getModel();
        int selectedIndex=table5.getSelectedRow();
        
        txteid.setText(Df.getValueAt(selectedIndex, 0).toString());
        txtename.setText(Df.getValueAt(selectedIndex, 1).toString());
        txtetele.setText(Df.getValueAt(selectedIndex, 2).toString());
        txteadd.setText(Df.getValueAt(selectedIndex, 3).toString());
        txtposition.setSelectedItem(Df.getValueAt(selectedIndex, 4).toString());
        txtesalary.setText(Df.getValueAt(selectedIndex, 5).toString());
        txtassign.setText(Df.getValueAt(selectedIndex, 6).toString());
        
        
    }                                   

    private void txtesalaryActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // TODO add your handling code here:
    }                                          

    private void txteaddActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here:
    }                                       

    private void txteteleActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void txtenameActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    }                                        

    private void txteidActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // TODO add your handling code here:
    }                                      

    private void jPanelMouseClicked(java.awt.event.MouseEvent evt) {                                     
        // TODO add your handling code here:
                txteid.setText("");
                txtename.setText("");
                txtetele.setText("");
                txteadd.setText("");
                txtesalary.setText("");
                txtposition.setSelectedItem("Other");
                txtassign.setText("");
                txteid.requestFocus();
    }                                    

    private void addMouseClicked(java.awt.event.MouseEvent evt) {                                 
        // TODO add your handling code here:
     	String eid=txteid.getText();
        String ename=txtename.getText();
        String etele=txtetele.getText();
        String eadd=txteadd.getText();
        String epos=(String) txtposition.getSelectedItem();
        int esal=Integer.parseInt(txtesalary.getText());
        String assign=txtassign.getText();
        if(eid.equals("")){
            JOptionPane.showMessageDialog(this,"Enter Any Record");
        }else{
        
	try{
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            
           try{
            con1 = DriverManager.getConnection("");
            insert= con1.prepareStatement("insert into employee(empID,empName,empTelephone,empAddress,empPosition,empSallary,assigned)values(?,?,?,?,?,?,?)");
            insert.setString(1,eid);
            insert.setString(2,ename);
            insert.setString(3,etele);
            insert.setString(4,eadd);
            insert.setString(5,epos);
            insert.setInt(6,esal);
            insert.setString(7,assign);
            insert.executeUpdate();
            }
            catch(SQLException sqle) {
                System.out.println("Sql Exception :"+sqle.getMessage());
            }
         }
         catch(ClassNotFoundException e) {
            System.out.println("Class Not Found Exception :" + e.getMessage());
         }
        }
        txteid.setText("");
        txtename.setText("");
        txtetele.setText("");
        txteadd.setText("");
        txtesalary.setText("");
        txtposition.setSelectedItem("Other");
        txtassign.setText("");
        txteid.requestFocus();
    }                                                             

    private void removeMouseClicked(java.awt.event.MouseEvent evt) {                                    
        // TODO add your handling code here:
       DefaultTableModel Df=(DefaultTableModel)table.getModel();
       int selectedIndex=table.getSelectedRow();
       String eid=txteid.getText();
       if(eid.equals("")){
            JOptionPane.showMessageDialog(this,"Select Any Record");
        }else{
       try{
            int dialogResult= JOptionPane.showConfirmDialog(null,"Do you wnt to delete the Record","Warning",JOptionPane.YES_NO_OPTION);
            if(dialogResult==JOptionPane.YES_OPTION)
            {
                
                Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
                try{
                con1 = DriverManager.getConnection("");
                insert= con1.prepareStatement("delete from employee where empID=?");
                
                insert.setString(1,eid);
                insert.executeUpdate();
                
                JOptionPane.showMessageDialog(this,"Record Deleted Succesfuly");
                tableupdate();

                
                }catch(SQLException sqle) {
                System.out.println("Sql Exception :"+sqle.getMessage());
                }
            }

            }catch(ClassNotFoundException e) {
            System.out.println("Class Not Found Exception :" + e.getMessage());
            }
       }
                txteid.setText("");
                txtename.setText("");
                txtetele.setText("");
                txteadd.setText("");
                txtesalary.setText("");
                txtposition.setSelectedItem("Other");
                txtassign.setText("");
                txteid.requestFocus();
    }                             

    private void updateMouseClicked(java.awt.event.MouseEvent evt) {                                    
        // TODO add your handling code here:
         DefaultTableModel Df=(DefaultTableModel)table.getModel();
       int selectedIndex=table.getSelectedRow();
       String eid=txteid.getText();
            String ename=txtename.getText();
            String etele=txtetele.getText();
            String eadd=txteadd.getText();
            String epos=(String) txtposition.getSelectedItem();
            int esal=Integer.parseInt(txtesalary.getText());
            String assign=txtassign.getText();
       if(eid.equals("")){
            JOptionPane.showMessageDialog(this,"Select Any Record");
        }else{
       try{
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver"); 
            
           
           try{
            con1 = DriverManager.getConnection("");
            insert= con1.prepareStatement("update employee set empName=?,empTelephone=?,empAddress=?,empPosition=?,empSallary=?,assigned=? where empID=?");
            insert.setString(1,ename);
            insert.setString(2,etele);
            insert.setString(3,eadd);
            insert.setString(4,epos);
            insert.setInt(5,esal);
            insert.setString(6,assign);
            insert.setString(7,eid);
            insert.executeUpdate();
            }
            
            catch(SQLException sqle) {
                System.out.println("Sql Exception :"+sqle.getMessage());
            }

         }
         catch(ClassNotFoundException e) {
            System.out.println("Class Not Found Exception :" + e.getMessage());
         }
       JOptionPane.showMessageDialog(this,"Record Updated Succesfuly");
       }
        txteid.setText("");
        txtename.setText("");
        txtetele.setText("");
        txteadd.setText("");
        txtesalary.setText("");
        txtposition.setSelectedItem("Other");
        txtassign.setText("");
        txteid.requestFocus();
    } 
    private void disposeMouseEntered(java.awt.event.MouseEvent evt) {                                     
        // TODO add your handling code here:

    }                                    

    private void disposeMouseExited(java.awt.event.MouseEvent evt) {                                    
        // TODO add your handling code here:

    }                                   

    private void txtassignActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
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
            java.util.logging.Logger.getLogger(Employee.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(Employee.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(Employee.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(Employee.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            @Override
            public void run() {
                new Employee().setVisible(true);
            }
        });
    }
