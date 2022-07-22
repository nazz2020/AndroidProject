# AndroidProject
Free Easy and Simple Source Code of Awesome Tic Tac -Toe Game App is written below,

MainActivity.java:
package com.example.tic_tac_toe;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;  
import android.view.View;  
import android.widget.Button;  
import android.widget.TextView;  
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements View.OnClickListener{  
    private Button[][] buttons = new Button[3][3];  
    private boolean player1Turn = true;  
    private int roundCount;  
    private int player1Points;  
    private int player2Points;  
    private TextView textViewPlayer1;  
    private TextView textViewPlayer2;  


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textViewPlayer1 = findViewById(R.id.text_view_p1);
        textViewPlayer2 = findViewById(R.id.text_view_p2);
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                String buttonID = “button_” + i + j;
                int resID = getResources().getIdentifier(buttonID, “id”, getPackageName());
                buttons[i][j] = findViewById(resID);
                buttons[i][j].setOnClickListener(this);
            }
        }
        Button buttonReset = findViewById(R.id.button_reset);
        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
            }
        });
    }
    @Override
    public void onClick(View v) {
        if (!((Button) v).getText().toString().equals(“”)) {
            return;
        }
        if (player1Turn) {
            ((Button) v).setText(“X”);
        } else {
            ((Button) v).setText(“O”);
        }
        roundCount++;
        if (checkForWin()) {
            if (player1Turn) {
                player1Wins();
            } else {
                player2Wins();
            }
        } else if (roundCount == 9) {
            draw();
        } else {
            player1Turn = !player1Turn;
        }
    }
    private boolean checkForWin() {
        String[][] field = new String[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                field[i][j] = buttons[i][j].getText().toString();
            }
        }
        for (int i = 0; i < 3; i++) {
            if (field[i][0].equals(field[i][1])
                    && field[i][0].equals(field[i][2])
                    && !field[i][0].equals(“”)) {
                return true;
            }
        }
        for (int i = 0; i < 3; i++) {
            if (field[0][i].equals(field[1][i])
                    && field[0][i].equals(field[2][i])
                    && !field[0][i].equals(“”)) {
                return true;
            }
        }
        if (field[0][0].equals(field[1][1])
                && field[0][0].equals(field[2][2])
                && !field[0][0].equals(“”)) {
            return true;
        }
        if (field[0][2].equals(field[1][1])
                && field[0][2].equals(field[2][0])
                && !field[0][2].equals(“”)) {
            return true;
        }
        return false;
    }
    private void player1Wins() {
        player1Points++;
        Toast.makeText(this, “Player 1 wins!”, Toast.LENGTH_SHORT).show();
        updatePointsText();
        resetBoard();
    }
    private void player2Wins() {
        player2Points++;
        Toast.makeText(this, “Player 2 wins!”, Toast.LENGTH_SHORT).show();
        updatePointsText();
        resetBoard();
    }
    private void draw() {
        Toast.makeText(this, “Draw!”, Toast.LENGTH_SHORT).show();
        resetBoard();
    }
    private void updatePointsText() {
        textViewPlayer1.setText(“Player 1: ” + player1Points);
        textViewPlayer2.setText(“Player 2: ” + player2Points);
    }
    private void resetBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                buttons[i][j].setText(“”);
            }
        }
        roundCount = 0;
        player1Turn = true;


    }
}

# activity_main.xml:
<?xml version=”1.0″ encoding=”utf-8″?>

<LinearLayout xmlns:android=”http://schemas.android.com/apk/res/android”

xmlns:app=”http://schemas.android.com/apk/res-auto”

xmlns:tools=”http://schemas.android.com/tools”

android:layout_width=”match_parent”

android:layout_height=”match_parent”

android:orientation=”vertical”

tools:context=”.MainActivity”>



<RelativeLayout

    android:layout_width=”match_parent”

    android:layout_height=”wrap_content”>



    <TextView

        android:id=”@+id/text_view_p1″

        android:layout_width=”wrap_content”

        android:layout_height=”wrap_content”

        android:text=”Player 1: 0″

        android:textSize=”30sp” />



    <TextView

        android:id=”@+id/text_view_p2″

        android:layout_width=”wrap_content”

        android:layout_height=”wrap_content”

        android:layout_below=”@+id/text_view_p1″

        android:text=”Player 2: 0″

        android:textSize=”30sp” />



    <Button

        android:id=”@+id/button_reset”

        android:layout_width=”wrap_content”

        android:layout_height=”wrap_content”

        android:layout_alignParentEnd=”true”

        android:layout_centerVertical=”true”

        android:layout_marginEnd=”33dp”

        android:background=”#D0DD50″

        android:text=”reset” />



</RelativeLayout>



<LinearLayout

    android:layout_width=”match_parent”

    android:layout_height=”0dp”

    android:layout_weight=”1″>



    <Button

        android:id=”@+id/button_00″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:layout_margin=”3dp”

        android:background=”#D0DD50″

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_01″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:layout_margin=”3dp”

        android:background=”#D0DD50″

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_02″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:layout_margin=”3dp”

        android:background=”#D0DD50″

        android:textSize=”60sp” />



</LinearLayout>



<LinearLayout

    android:layout_width=”match_parent”

    android:layout_height=”0dp”

    android:layout_weight=”1″>



    <Button

        android:id=”@+id/button_10″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:layout_margin=”3dp”

        android:background=”#D0DD50″

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_11″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:background=”#D0DD50″

        android:layout_margin=”3dp”

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_12″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:background=”#D0DD50″

        android:layout_margin=”3dp”

        android:textSize=”60sp” />



</LinearLayout>



<LinearLayout

    android:layout_width=”match_parent”

    android:layout_height=”0dp”

    android:layout_weight=”1″>



    <Button

        android:id=”@+id/button_20″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:background=”#D0DD50″

        android:layout_margin=”3dp”

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_21″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:background=”#D0DD50″

        android:layout_margin=”3dp”

        android:textSize=”60sp” />



    <Button

        android:id=”@+id/button_22″

        android:layout_width=”0dp”

        android:layout_height=”match_parent”

        android:layout_weight=”1″

        android:background=”#D0DD50″

        android:layout_margin=”3dp”

        android:textSize=”60sp” />


</LinearLayout>

</LinearLayout>

Output:
Easy Source Code of Awesome Tic Tac -Toe Game App
Easy Source Code of Awesome Tic Tac -Toe Game App
Easy Source Code of Awesome Tic Tac -Toe Game App
I Think You Understand above Topic “Simple Source Code of Awesome Tic Tac -Toe Game App”.
For any query or suggestions feel free to fill comment section and send it.
