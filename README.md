import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class CalculatorGUI extends JFrame implements ActionListener {
    private JTextField textField;
    private JButton[] numberButtons;
    private JButton[] functionButtons;
    private JButton addButton, subButton, mulButton, divButton;
    private JButton sinButton, cosButton, logButton;
    private JButton equalButton, clearButton, dotButton;
    private JPanel panel;

    private double num1 = 0, num2 = 0, result = 0;
    private char operator;

    public CalculatorGUI() {
        this.setTitle("Scientific Calculator");
        this.setSize(400, 500);
        this.setLayout(null);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        textField = new JTextField();
        textField.setBounds(30, 40, 340, 30);
        textField.setEditable(false);
        this.add(textField);

        numberButtons = new JButton[10];
        functionButtons = new JButton[9];

        panel = new JPanel();
        panel.setBounds(30, 100, 340, 340);
        panel.setLayout(new GridLayout(5, 4, 10, 10));

        for (int i = 0; i < 10; i++) {
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            panel.add(numberButtons[i]);
        }

        addButton = new JButton("+");
        subButton = new JButton("-");
        mulButton = new JButton("*");
        divButton = new JButton("/");
        sinButton = new JButton("sin");
        cosButton = new JButton("cos");
        logButton = new JButton("log");
        equalButton = new JButton("=");
        clearButton = new JButton("C");
        dotButton = new JButton(".");
        
        functionButtons[0] = addButton;
        functionButtons[1] = subButton;
        functionButtons[2] = mulButton;
        functionButtons[3] = divButton;
        functionButtons[4] = sinButton;
        functionButtons[5] = cosButton;
        functionButtons[6] = logButton;
        functionButtons[7] = equalButton;
        functionButtons[8] = clearButton;
        
        for (int i = 0; i < 9; i++) {
            functionButtons[i].addActionListener(this);
            panel.add(functionButtons[i]);
        }
        
        dotButton.addActionListener(this);
        panel.add(dotButton);

        this.add(panel);
        this.setVisible(true);
    }

    public static void main(String[] args) {
        new CalculatorGUI();
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        for (int i = 0; i < 10; i++) {
            if (e.getSource() == numberButtons[i]) {
                textField.setText(textField.getText() + i);
            }
        }
        
        if (e.getSource() == dotButton) {
            textField.setText(textField.getText() + ".");
        }

        if (e.getSource() == addButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '+';
            textField.setText("");
        }

        if (e.getSource() == subButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '-';
            textField.setText("");
        }

        if (e.getSource() == mulButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '*';
            textField.setText("");
        }

        if (e.getSource() == divButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '/';
            textField.setText("");
        }

        if (e.getSource() == sinButton) {
            num1 = Double.parseDouble(textField.getText());
            result = Math.sin(Math.toRadians(num1));
            textField.setText(String.valueOf(result));
        }

        if (e.getSource() == cosButton) {
            num1 = Double.parseDouble(textField.getText());
            result = Math.cos(Math.toRadians(num1));
            textField.setText(String.valueOf(result));
        }

        if (e.getSource() == logButton) {
            num1 = Double.parseDouble(textField.getText());
            result = Math.log(num1);
            textField.setText(String.valueOf(result));
        }

        if (e.getSource() == equalButton) {
            num2 = Double.parseDouble(textField.getText());

            switch (operator) {
                case '+':
                    result = num1 + num2;
                    break;
                case '-':
                    result = num1 - num2;
                    break;
                case '*':
                    result = num1 * num2;
                    break;
                case '/':
                    result = num1 / num2;
                    break;
            }

            textField.setText(String.valueOf(result));
        }

        if (e.getSource() == clearButton) {
            textField.setText("");
        }
    }
}
