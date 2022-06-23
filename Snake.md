package hiss;

import java.awt.*;
import java.awt.event.*;


public class snake  extends Rectangle{
	
	double speed= 5;
	
	boolean left= false;
	boolean right= true;
	boolean up= false;
	boolean down= false;
	
	boolean purp = false;
	
	snake(int x, int y, int HEIGHT, int WIDTH){
		super(x,y,WIDTH,HEIGHT);
	}
	
	public void KeyPressed(KeyEvent e) {
		if (e.getKeyCode()== KeyEvent.VK_W) {
			if(!down) {
				left = false;
				right = false;
				up = true;
				down = false;
			}
		}
		if (e.getKeyCode()== KeyEvent.VK_S) {
			if(!up) {
				left = false;
				right = false;
				up = false;
				down = true;
			}
			
		}if (e.getKeyCode()== KeyEvent.VK_D) {
			if(!left) {
				left = false;
				right = true;
				up = false;
				down = false;
			}
		}
		if (e.getKeyCode()== KeyEvent.VK_A) {
			if(!right) {
				left = true;
				right = false;
				up = false;
				down = false;
			}
		}
	}
	public void move() {
		if (left) {
			x -= speed;
		}else if(right) {
			x += speed;
		}else if (down) {
			y += speed;
		}else if(up) {
			y -= speed;
		}
		
	}
	
	public void draw(Graphics g) {
		if(purp) {
			g.setColor(new Color(100, 0,255));
		}else {
			g.setColor(new Color(123,63,70));
		}
		g.fillRect(x,y,width, height);
	}

	
}
