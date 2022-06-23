package hiss;

import java.awt.*;

public class Score extends Rectangle{
	static int GAME_WIDTH;
	static int GAME_HEIGHT;
	
	int points = 0;
	int heighScore = 0;
	
	Score(int GAME_WIDTH, int GAME_HEIGHT){
		Score.GAME_WIDTH= GAME_WIDTH;
		Score.GAME_HEIGHT= GAME_HEIGHT;
	}
	
	public void draw(Graphics g) {
		
		g.setColor(new Color(255,255,255));
		g.setFont(new Font("Dialog",Font.PLAIN, 40));
		g.drawString("Score "+ String.valueOf(points/10)+String.valueOf(points%10), 10, 50);
		
		
		
	}
}
