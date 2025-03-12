import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.sql.*;

public class DiagnosticLabManagement extends JFrame {
    private JTextField nameField, ageField, contactField;
    private JComboBox<String> genderBox;
    private JTextArea resultArea;
    private Connection conn;

    public DiagnosticLabManagement() {
        setTitle("Diagnostic Laboratory Management System");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());

        // Labels and Inputs
        add(new JLabel("Patient Name:"));
        nameField = new JTextField(15);
        add(nameField);

        add(new JLabel("Age:"));
        ageField = new JTextField(5);
        add(ageField);

        add(new JLabel("Gender:"));
        genderBox = new JComboBox<>(new String[]{"Male", "Female", "Other"});
        add(genderBox);

        add(new JLabel("Contact:"));
        contactField = new JTextField(10);
        add(contactField);

        JButton addButton = new JButton("Add Patient");
        JButton viewButton = new JButton("View Patients");
        add(addButton);
        add(viewButton);

        resultArea = new JTextArea(10, 40);
        add(new JScrollPane(resultArea));

        // Database Connection
        try {
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/dlm", "root", "password");
            System.out.println("Database Connected!");
        } catch (Exception e) {
            e.printStackTrace();
        }

        // Button Actions
        addButton.addActionListener(e -> addPatient());
        viewButton.addActionListener(e -> viewPatients());
    }

    // Add patient to database
    private void addPatient() {
        try {
            String sql = "INSERT INTO patients (name, age, gender, contact) VALUES (?, ?, ?, ?)";
            PreparedStatement stmt = conn.prepareStatement(sql);
            stmt.setString(1, nameField.getText());
            stmt.setInt(2, Integer.parseInt(ageField.getText()));
            stmt.setString(3, genderBox.getSelectedItem().toString());
            stmt.setString(4, contactField.getText());
            stmt.executeUpdate();
            JOptionPane.showMessageDialog(this, "Patient Added Successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // View patients from database
    private void viewPatients() {
        try {
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM patients");
            resultArea.setText("ID\tName\tAge\tGender\tContact\n");
            while (rs.next()) {
                resultArea.append(rs.getInt("id") + "\t" + rs.getString("name") + "\t" + rs.getInt("age") + "\t" +
                        rs.getString("gender") + "\t" + rs.getString("contact") + "\n");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new DiagnosticLabManagement().setVisible(true));
    }
}
