package hiss;

import java.awt.*;

import javax.swing.*;

public class Frame extends JFrame{
	
	logic panel;
	
	Frame(){
		panel = new logic();
		
		this.setTitle("Snake");
		this.add(panel);
		this.setResizable(false);
		this.setBackground(new Color(42,204,73));
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		this.pack();
		this.setVisible(true);
		this.setLocationRelativeTo(null);
	}
}
