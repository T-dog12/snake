import java.awt.*;

import javax.swing.*;

public class Bar {
	
	static int GAME_WIDTH;
	static int GAME_HEIGHT;
	
	Bar(int GAME_WIDTH, int GAME_HEIGHT){
		Score.GAME_WIDTH= GAME_WIDTH;
		Score.GAME_HEIGHT= GAME_HEIGHT;
	}
	
	public void draw(Graphics g) {
		g.setColor(new Color(0,0,0));
		g.fillRect(GAME_WIDTH, GAME_HEIGHT , 1000, 75);
	}
}
