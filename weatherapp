package com.mycompany.weather_app;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import org.json.JSONObject;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;

public class Weather_App {
    private static final String API_KEY = "ULAG5VX6MAF47PDFP8J7G2PDQ";  // Replace with your Visual Crossing API key
    private static final String BASE_URL = "https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/";

    public static void main(String[] args) {
        JFrame frame = new JFrame("Weather App");
        frame.setSize(700, 400);  // Uniform window size for all pages
        frame.setLocationRelativeTo(null);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new CardLayout());

        // Create CardLayout container
        JPanel cardPanel = new JPanel(new CardLayout());

        // Create panels for each "page"
        JPanel loginPage = createLoginPage(cardPanel);
        JPanel signUpPage = createSignUpPage(cardPanel);
        JPanel inputPage = createInputPage(cardPanel, frame);
        JPanel resultPage = createResultPage();

        // Add pages to CardLayout panel
        cardPanel.add(loginPage, "LoginPage");
        cardPanel.add(signUpPage, "SignUpPage");
        cardPanel.add(inputPage, "InputPage");
        cardPanel.add(resultPage, "ResultPage");

        // Add CardLayout panel to frame
        frame.add(cardPanel);
        frame.setVisible(true);
    }

    // Create Login Page
    private static JPanel createLoginPage(JPanel cardPanel) {
        JPanel panel = new JPanel(new GridLayout(3, 2));
        panel.setBackground(new Color(240, 240, 240));  // Subtle background color

        JLabel userLabel = new JLabel("Username:");
        JLabel passLabel = new JLabel("Password:");
        JTextField userField = new JTextField(8);
        JPasswordField passField = new JPasswordField(8);

        // Set focus color for selected text field
        userField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
        passField.setBorder(BorderFactory.createLineBorder(Color.GRAY));

        userField.addFocusListener(new java.awt.event.FocusAdapter() {
            public void focusGained(java.awt.event.FocusEvent evt) {
                userField.setBorder(BorderFactory.createLineBorder(Color.BLUE));
            }

            public void focusLost(java.awt.event.FocusEvent evt) {
                userField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            }
        });

        passField.addFocusListener(new java.awt.event.FocusAdapter() {
            public void focusGained(java.awt.event.FocusEvent evt) {
                passField.setBorder(BorderFactory.createLineBorder(Color.BLUE));
            }

            public void focusLost(java.awt.event.FocusEvent evt) {
                passField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            }
        });

        JButton loginButton = new JButton("Login");
        JButton signUpButton = new JButton("Sign Up");

        loginButton.setBackground(new Color(100, 149, 237));
        loginButton.setForeground(Color.WHITE);

        signUpButton.setBackground(new Color(255, 69, 0));
        signUpButton.setForeground(Color.WHITE);

        panel.add(userLabel);
        panel.add(userField);
        panel.add(passLabel);
        panel.add(passField);
        panel.add(signUpButton);
        panel.add(loginButton);

        loginButton.addActionListener(e -> {
            String username = userField.getText();
            String password = new String(passField.getPassword());
            if (UserService.loginUser(username, password)) {
                JOptionPane.showMessageDialog(panel, "Login successful!");
                CardLayout layout = (CardLayout) cardPanel.getLayout();
                layout.show(cardPanel, "InputPage");
            } else {
                JOptionPane.showMessageDialog(panel, "Invalid username or password!", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });

        signUpButton.addActionListener(e -> {
            CardLayout layout = (CardLayout) cardPanel.getLayout();
            layout.show(cardPanel, "SignUpPage");
        });

        return panel;
    }

    // Create Sign-Up Page
    private static JPanel createSignUpPage(JPanel cardPanel) {
        JPanel panel = new JPanel(new GridLayout(4, 2));
        panel.setBackground(new Color(240, 240, 240));

        JLabel userLabel = new JLabel("Username:");
        JLabel passLabel = new JLabel("Password:");
        JLabel confirmPassLabel = new JLabel("Confirm Password:");
        JTextField userField = new JTextField(10);
        JPasswordField passField = new JPasswordField(10);
        JPasswordField confirmPassField = new JPasswordField(10);

        // Set focus color for selected text field
        userField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
        passField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
        confirmPassField.setBorder(BorderFactory.createLineBorder(Color.GRAY));

        userField.addFocusListener(new java.awt.event.FocusAdapter() {
            public void focusGained(java.awt.event.FocusEvent evt) {
                userField.setBorder(BorderFactory.createLineBorder(Color.BLUE));
            }

            public void focusLost(java.awt.event.FocusEvent evt) {
                userField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            }
        });

        passField.addFocusListener(new java.awt.event.FocusAdapter() {
            public void focusGained(java.awt.event.FocusEvent evt) {
                passField.setBorder(BorderFactory.createLineBorder(Color.BLUE));
            }

            public void focusLost(java.awt.event.FocusEvent evt) {
                passField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            }
        });

        confirmPassField.addFocusListener(new java.awt.event.FocusAdapter() {
            public void focusGained(java.awt.event.FocusEvent evt) {
                confirmPassField.setBorder(BorderFactory.createLineBorder(Color.BLUE));
            }

            public void focusLost(java.awt.event.FocusEvent evt) {
                confirmPassField.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            }
        });

        JButton registerButton = new JButton("Register");
        JButton backButton = new JButton("Back");

        registerButton.setBackground(new Color(100, 149, 237));
        registerButton.setForeground(Color.WHITE);

        backButton.setBackground(new Color(255, 69, 0));
        backButton.setForeground(Color.WHITE);

        panel.add(userLabel);
        panel.add(userField);
        panel.add(passLabel);
        panel.add(passField);
        panel.add(confirmPassLabel);
        panel.add(confirmPassField);
        panel.add(backButton);
        panel.add(registerButton);

        registerButton.addActionListener(e -> {
            String username = userField.getText();
            String password = new String(passField.getPassword());
            String confirmPassword = new String(confirmPassField.getPassword());
            if (!password.equals(confirmPassword)) {
                JOptionPane.showMessageDialog(panel, "Passwords do not match!", "Error", JOptionPane.ERROR_MESSAGE);
            } else if (UserService.registerUser(username, password)) {
                JOptionPane.showMessageDialog(panel, "Registration successful!");
                CardLayout layout = (CardLayout) cardPanel.getLayout();
                layout.show(cardPanel, "LoginPage");
            } else {
                JOptionPane.showMessageDialog(panel, "Registration failed!", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });

        backButton.addActionListener(e -> {
            CardLayout layout = (CardLayout) cardPanel.getLayout();
            layout.show(cardPanel, "LoginPage");
        });

        return panel;
    }

    // Create Input Page
    private static JPanel createInputPage(JPanel cardPanel, JFrame parentFrame) {
    JPanel panel = new JPanel(new GridBagLayout()) {
        // Override paintComponent to draw the background image
        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            try {
                // Load and draw the background image
                BufferedImage backgroundImage = ImageIO.read(new File("C:\\Users\\ujjst\\Downloads\\wallpaperflare.com_wallpaper.jpg")); // Change path if needed
                g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), null);
            } catch (IOException e) {
                e.printStackTrace();  // Handle any error loading the image
            }
        }
    };

    panel.setLayout(new GridBagLayout());  // Use GridBagLayout
    panel.setOpaque(false);  // Make sure panel itself is transparent so background is visible

    GridBagConstraints gbc = new GridBagConstraints();
    gbc.insets = new Insets(10, 10, 10, 10);
    gbc.gridx = 0;
    gbc.gridy = 0;
    gbc.anchor = GridBagConstraints.CENTER;

    JLabel instructionLabel = new JLabel("Enter Location :");
    instructionLabel.setFont(new Font("Arial", Font.PLAIN, 14));
    instructionLabel.setForeground(Color.WHITE);  // White text color for contrast on the button-like label
    instructionLabel.setHorizontalAlignment(SwingConstants.CENTER);

    // Set background color and border to make it look like a button
    instructionLabel.setOpaque(true);  // Make sure the background color is visible
    instructionLabel.setBackground(new Color(100, 149, 237));  // Button-like background color
    instructionLabel.setPreferredSize(new Dimension(150, 30));
    instructionLabel.setBorder(BorderFactory.createCompoundBorder(
        BorderFactory.createLineBorder(new Color(173, 172, 166), 2),  // Button border color
        BorderFactory.createEmptyBorder(10, 20, 10, 20)  // Padding inside the label to make it look like a button
    ));

    // Add the button-like label to the panel
    panel.add(instructionLabel, gbc);

    gbc.gridy = 1;
    JTextField locationField = new JTextField(15);
    locationField.setHorizontalAlignment(SwingConstants.CENTER);
    panel.add(locationField, gbc);

    gbc.gridy = 2;
    JButton getWeatherButton = new JButton("Get Weather");
    getWeatherButton.setPreferredSize(new Dimension(150, 30));
    getWeatherButton.setBackground(new Color(100, 149, 237));
    getWeatherButton.setForeground(Color.WHITE);
    panel.add(getWeatherButton, gbc);

    getWeatherButton.addActionListener(e -> {
        String location = locationField.getText().trim();
        if (!location.isEmpty()) {
            String weatherData = getWeatherData(location);
            if (weatherData != null) {
                updateResultPage(cardPanel, location, weatherData);  // Pass data to the result page
                CardLayout layout = (CardLayout) cardPanel.getLayout();
                layout.show(cardPanel, "ResultPage");  // Switch to the result page
            } else {
                JOptionPane.showMessageDialog(panel, "Invalid location or unable to retrieve weather data.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        } else {
            JOptionPane.showMessageDialog(panel, "Please enter a valid location.", "Warning", JOptionPane.WARNING_MESSAGE);
        }
    });

    return panel;
}

    // Create Result Page
    private static JPanel createResultPage() {
        JPanel panel = new JPanel(new GridLayout(6, 2, 10, 10));

        panel.add(new JLabel("Location:"));
        panel.add(new JLabel());  // Placeholder for location value

        panel.add(new JLabel("Temperature:"));
        panel.add(new JLabel());  // Placeholder for temperature value

        panel.add(new JLabel("Conditions:"));
        panel.add(new JLabel());  // Placeholder for conditions value

        panel.add(new JLabel("Humidity:"));
        panel.add(new JLabel());  // Placeholder for humidity value

        panel.add(new JLabel("Wind Speed:"));
        panel.add(new JLabel());  // Placeholder for wind speed value

        // Add Back button to go to the input page
        JButton backButton = new JButton("Back");
        backButton.setBackground(new Color(255, 69, 0));  
        backButton.addActionListener(e -> {
            JPanel parentPanel = (JPanel) panel.getParent();
            CardLayout layout = (CardLayout) parentPanel.getLayout();
            layout.show(parentPanel, "InputPage");

            // Clear the text field on the input page
            JTextField locationField = (JTextField) ((JPanel) parentPanel.getComponent(2)).getComponent(1);
            locationField.setText("");  // Clear the location field
        });
        panel.add(new JLabel());  // Empty cell for spacing
        panel.add(backButton);

        return panel;
    }

    // Method to update Result Page with fetched weather data
    private static void updateResultPage(JPanel cardPanel, String location, String weatherData) {
        JPanel resultPage = (JPanel) cardPanel.getComponent(3);  // Get the result page panel

        JSONObject json = new JSONObject(weatherData);
        JSONObject currentConditions = json.getJSONObject("currentConditions");

        double temperature = currentConditions.getDouble("temp");
        String conditions = currentConditions.getString("conditions");
        double humidity = currentConditions.getDouble("humidity");
        double windSpeed = currentConditions.getDouble("windspeed");

        // Update labels with fetched data
        ((JLabel) resultPage.getComponent(1)).setText(location);
        ((JLabel) resultPage.getComponent(3)).setText(String.format("%.2f °C", temperature));
        ((JLabel) resultPage.getComponent(5)).setText(conditions);
        ((JLabel) resultPage.getComponent(7)).setText(String.format("%.2f%%", humidity));
        ((JLabel) resultPage.getComponent(9)).setText(String.format("%.2f km/h", windSpeed));

    }

    // Method to get weather data from Visual Crossing API
    private static String getWeatherData(String location) {
        String urlString = BASE_URL + location + "?unitGroup=metric&key=" + API_KEY;
        try {
            URL url = new URL(urlString);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");

            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            in.close();
            connection.disconnect();

            return content.toString();
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
    // MySQL Database Connection
class DBConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/WeatherAppDB";
    private static final String USER = "root";
    private static final String PASS = "u$$ayM2005";

    public static Connection connect() {
        try {
            Connection conn = DriverManager.getConnection(URL, USER, PASS);
            return conn;
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
}

// User Service for login and sign-up
class UserService {

    public static boolean registerUser(String username, String password) {
        String sql = "INSERT INTO users (username, password) VALUES (?, md5(?))";
        try (Connection conn = DBConnection.connect(); 
            PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, username);
            pstmt.setString(2, password);
            pstmt.executeUpdate();
            return true;
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

    public static boolean loginUser(String username, String password) {
        String sql = "SELECT * FROM users WHERE username = ? AND password = md5(?) ";
        try (Connection conn = DBConnection.connect(); PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, username);
            pstmt.setString(2, password);
            ResultSet rs = pstmt.executeQuery();
            return rs.next();
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }
} 
}
