#ifndef GAME_H
#define GAME_H

#include <GL/freeglut.h>
#include <GL/gl.h>
#include <iostream>
#include "Square.h"
#include "Button.h"

class Game{

private:
    Square **r;
    int count;

    SquareState player; 

    Button button3;
    Button button4;
    Button button5; 
    Button start; 
    Button artificial; 
    Button human; 

    Button tie; 

    Button restart; 
    Button quit; 
    Button xWins; 
    Button oWins; 

    bool gameEnded = false; 
    bool gameStarted = false; 
    bool playerX; 
    bool AI = false; 
   


    void init(){

        r = new Square*[count];
        for (int i = 0; i < count; i++){
            r[i] = new Square[count];
        }

        float x = -0.9;
        float y = 0.9;

      float size = 1.6 / count;
        for (int i = 0; i < count; i++){
            x = -0.9;
            for (int j = 0; j < count; j++){
                r[i][j] = Square(x, y, size);
                x += size;
            }
            y -= size;
        }
    }
public:
    Game(){

        button3 = Button("3 x 3", -0.9, -0.75);
        button4 = Button("4 x 4", -0.5, -0.75);
        button5 = Button("5 x 5", -0.1, -0.75);
        start = Button("Start",0.5,-0.75);
        artificial = Button("Play with AI", -0.9,-0.5);
        human = Button("Play with another",-0.05,-0.5);
        quit = Button("Quit game",-0.9,-0.75);
        restart = Button("Restart game", -0.3,-0.75);
        xWins = Button("X WINS",0.0,0.5);
        oWins = Button("O WINS",0.0,0.5);
        tie = Button("TIE",0.0,0.5);
        
        playerX = false; 
        count = 3;
        init();
        button3.pressed = true; 
        human.pressed = true;
        
    }  

    void artificialMove(){
            if(!playerX){
                for (int i = 0; i < count; i++){ 
                    for (int j = 0; j < count; j++){
                        if(r[i][j].isEmpty()){
                            r[i][j].playO();
                            winner(PLAYER_O);
                            full();
                            playerX =!playerX;
                            return;
                        }
                    }
                }
            }
        }


   bool winner(SquareState player){
       if (rightDiag(player)|| leftDiag(player)||checkX(player)||checkY(player)){
           gameEnded = true; 
           return true; 
       } 
       return false; 
   } 

   bool full(){
       int board = 0; 
       for (int i = 0; i < count; i++){
           for (int j = 0; j < count; j++){
               if (r[i][j].isEmpty()){
                   board++;
               }
           }
       }
       if (board == 0){
           gameEnded = true; 
           return true;
       }
       else{
           return false;
       }
       
   }
    
    void leftMouseDown( float x, float y ){
        // Respond to left mouse down events
        if (button3.contains(x, y) && !gameStarted ){
            std::cout << "Will change to 3x3" << std::endl;
            for (int i = 0; i < count; i++){
                delete[] r[i];
            }
            button4.pressed = false; 
            button3.pressed = true; 
            button5.pressed = false; 
            delete[] r;
            count = 3;
            init();
        }
        else if (button4.contains(x, y) && !gameStarted ){
            std::cout << "Will change to 4x4" << std::endl;
            for (int i = 0; i < count; i++){
                delete[] r[i];
            } 
            button4.pressed = true; 
            button3.pressed = false; 
            button5.pressed = false; 
            delete[] r;
            count = 4;
            init();
        }
        else if (button5.contains(x, y) && !gameStarted ){
            std::cout << "Will change to 5x5" << std::endl;
            for (int i = 0; i < count; i++){
                delete[] r[i];
            }
            button4.pressed = false; 
            button3.pressed = false; 
            button5.pressed = true; 
            delete[] r;
            count = 5;
            init();
        } 
        else if(start.contains(x,y) && !gameStarted ){ 
            gameStarted = true; 
            start.pressed = true; 
            
        }  
        else if (artificial.contains(x,y) && !gameStarted ){
            AI = true;  
            artificial.pressed = true; 
            human.pressed = false; 
        }
        else if (human.contains(x,y) && !gameStarted ){ 
            AI = false; 
            artificial.pressed = false; 
            human.pressed = true; 
        } 

        else if (quit.contains(x,y) && gameEnded){ 
            exit(0);
        } 

        else if (restart.contains(x,y) && gameEnded){
            gameStarted = false; 
            gameEnded = false; 
            for (int i = 0; i < count; i++){
                delete[] r[i];
            } 
            delete r;  
            init();
        }

        if (gameStarted){
            for (int i = 0; i < count; i++){
                for (int j = 0; j < count; j++){
                    if (r[i][j].contains(x,y)){
                        if(r[i][j].isEmpty()){
                            if (playerX){
                                r[i][j].playX();
                                bool xWinner = winner(PLAYER_X);
                                full();
                            }
                            else{
                                r[i][j].playO();
                                winner(PLAYER_O); 
                                full();
                            }
                            playerX = !playerX;
                            std::cout << playerX << std::endl;
                            break;
                        }
                    }
                }
            }
            if (AI){
                artificialMove();
            }
        }
        } 
    bool checkX(SquareState player){
        int spaceCounter; 
        bool winner; 
        for (int i = 0; i < count; i++){
            spaceCounter = 0; 
            for(int j = 0; j < count; j ++){
                if (r[i][j].getState() == player){
                    spaceCounter++; 
                }
            }
            if (spaceCounter == count){
                return true;
            }
        }
        return false; 
    } 

    bool checkY(SquareState player){
        int spaceCounter; 
        bool winner; 
        for (int i = 0; i < count; i++){
            spaceCounter = 0; 
            for(int j = 0; j < count; j ++){
                if (r[j][i].getState() == player){
                    spaceCounter++; 
                }
            }
            if (spaceCounter == count){
                return true;
            }
        }
        return false; 
    } 

    bool rightDiag(SquareState player){
        int spaceCounter = 0; 
        bool winner; 
        for (int i = 0; i < count; i ++){
            if(r[count - 1 - i ][i].getState() == player){
                spaceCounter++; 
            }
        } 
        if (spaceCounter == count){
            return true; 
        }
        else{ 
            return false; 
        }
    }
    
    bool leftDiag(SquareState player){
        int spaceCounter = 0; 
        bool winner; 
        for (int i = 0; i < count; i ++){
            if(r[i][i].getState() == player){
                spaceCounter++; 
            }
        } 
        if (spaceCounter == count){
            return true; 
        }
        else{ 
            return false; 
        }
    }

    void render() {
        // Render some graphics
    if (!gameStarted){ 
        button3.draw();
        button4.draw();
        button5.draw();
        start.draw();
        artificial.draw();
        human.draw();
    } 
    else if(gameEnded){ 
        quit.draw();
        restart.draw(); 
    if(winner(PLAYER_O)){
        oWins.draw(); 
    }
    else if(winner(PLAYER_X)){
        xWins.draw();
    } 
    else {
        tie.draw();
    }
    }

    else{
        for (int i = 0; i < count; i++){
            for(int j = 0; j < count; j++){
                r[i][j].draw();
            }
        }
    }

    }
};

#endif
