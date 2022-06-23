package hiss;

import java.awt.*;
import java.awt.event.*;
import java.util.*;

import javax.swing.*;

public class logic extends JPanel implements Runnable{
	static final int GAME_WIDTH = 1000;
	static final int GAME_HEIGHT = (int) (GAME_WIDTH * (0.5555));
	static final Dimension SCREEN_SIZE = new Dimension (GAME_WIDTH,GAME_HEIGHT);
	static final int SNAKE_DIAM = 25;
	static final int FOOD_DIAM = 15;
	int foodX;
	int foodY;
	int delay= 0;
	int points= 0;
	
	
	ArrayList<snake> snakeParts = new ArrayList<snake>();
	
	Thread gameThread;
	Image image;
	Graphics graphics;
	Random ran = new Random();
	snake snake;
	Food food;
	Score Score;
	Bar Bar;
	HeighScore HeighScore = new HeighScore(GAME_WIDTH, GAME_HEIGHT);;
	
	logic(){
		this.setFocusable(true);
		this.addKeyListener(new AL());
		this.setPreferredSize(SCREEN_SIZE);
		
		newSnake();
		newFood();
		score();
		
		//allows multiple tasks to be performed at one time
		gameThread = new Thread(this);
		gameThread.start();
	}
	
	public void newSnake() {
		snakeParts.removeAll(snakeParts);
		snake = new snake(GAME_WIDTH/2,(GAME_HEIGHT/2)-(SNAKE_DIAM/2), SNAKE_DIAM, SNAKE_DIAM);
		snakeParts.add(snake);
		
		snake.purp = true;
	}
	public void newFood() {
		foodX = 85 +ran.nextInt(GAME_WIDTH-(SNAKE_DIAM+ 85));
		foodY = 85 +ran.nextInt(GAME_HEIGHT-(SNAKE_DIAM+ 85));
		
		food = new Food(foodX, foodY, FOOD_DIAM, FOOD_DIAM);
	}
	
	public void addSnake() {
		
		//clean up
		int a = snakeParts.size()-1;
		
		snake = new snake(snakeParts.get(a).x,snakeParts.get(a).y, SNAKE_DIAM, SNAKE_DIAM);
		snakeParts.add(snake);
	}
	public void score() {
		
		Bar = new Bar(GAME_WIDTH, GAME_HEIGHT);
		Score = new Score(GAME_WIDTH, GAME_HEIGHT);
	}
	
	public void paint(Graphics g) {
		image = createImage(getWidth(),getHeight());
		graphics = image.getGraphics();
		draw(graphics);
		g.drawImage(image,0,0,this);
	}
	
	public void draw(Graphics g) {
		Bar.draw(g);
		Score.draw(g);
		HeighScore.draw(g);
		food.draw(g);
		for(int i = snakeParts.size()-1; i >= 0; i--) {
			snakeParts.get(i).draw(g);
		}
		
	}
	
	public void checkCollision() {
		if (snakeParts.get(0).y >= (GAME_HEIGHT-SNAKE_DIAM)) {
			newSnake();
			newFood();
			score();
		}
		if (snakeParts.get(0).y <= 75) {
			newSnake();
			newFood();
			score();
		}
		
		if (snakeParts.get(0).x >= (GAME_WIDTH-SNAKE_DIAM)) {
			newSnake();
			newFood();
			score();
		}
		if (snakeParts.get(0).x <= 0) {
			newSnake();
			newFood();
			score();
		}
		if (snakeParts.size()> 10) {
			for (int x = 10; x < snakeParts.size(); x++) {
				if (snakeParts.get(0).intersects(snakeParts.get(x))) {
					newSnake();
					score();
				}
			}
		}
		
		if(snakeParts.get(0).intersects(food)) {
			
			snake.speed+= 0.01;
			
			for(int y= 0; y < 4; y++) {
				addSnake();
			}
			
			if(snake.purp) {
				snake.purp=false;
			}else {
				snake.purp=true;
			}
			
			newFood();
			Score.points +=1;
			
			if (Score.points > HeighScore.heighScore) {
				HeighScore.heighScore = Score.points;
			}
		}
	}
	public void move() {
		snakeParts.get(0).move();

		for(int z = snakeParts.size()-1; z>0; z--) {
			snakeParts.get(z).x =30- snakeParts.get(z - 1).x;
			snakeParts.get(z).y =30- snakeParts.get(z - 1).y;
		}
	}
	
	
	@Override
	public void run() {
		long lastTime = System.nanoTime();
		double amountOfTicks = 60.0;
		double ns = 1000000000 / amountOfTicks;
		double delta = 0;
		long repeat= 0;
		
		while(true) {
			long now = System.nanoTime();
			delta += (now - lastTime)/ ns;
			lastTime = now;
			//repeat +=1;
			
			if(delta >=1) {
				move();
				checkCollision();
				repaint();
				delta --;
			}
		
		}
	}
	public class AL extends KeyAdapter{
		public void keyPressed(KeyEvent e) {
			snakeParts.get(0).KeyPressed(e);
		}
	}
}
