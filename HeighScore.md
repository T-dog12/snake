package hiss;

import java.awt.*;

import ping.Score;

public class HeighScore {
	static int GAME_WIDTH;
	static int GAME_HEIGHT;
	
	int heighScore = 0;
	
	Score Score = new Score(heighScore, heighScore);
	
	HeighScore(int GAME_WIDTH, int GAME_HEIGHT){
		HeighScore.GAME_WIDTH= GAME_WIDTH;
		HeighScore.GAME_HEIGHT= GAME_HEIGHT;
	}
	public void draw(Graphics g) {
		
		g.setColor(new Color(255,255,255));
		g.setFont(new Font("Dialog",Font.PLAIN, 40));
		g.drawString("High Score "+ String.valueOf(heighScore/10)+String.valueOf(heighScore%10), 200, 50);
		
	}
}
