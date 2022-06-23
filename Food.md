package hiss;

import java.awt.*;

public class Food extends Rectangle {
	Food(int x, int y, int HEIGHT, int WIDTH){
		super(x,y,WIDTH,HEIGHT);
		
	}
	public void draw(Graphics g) {
		g.setColor(new Color(234,24,0));
		g.fillOval(x, y, width, height);
	}
}
