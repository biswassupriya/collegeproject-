# collegeproject-
android app
package com.example.supi.testapplication;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
//grade
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import android.widget.Toolbar;

import java.util.ArrayList;

public class gradeActivity extends AppCompatActivity {
    Button btnAdd;
    Button btnSummary;
    EditText txtGrade;
    String stgrade = null;
    public static ArrayList <Double>listOfGrades = new ArrayList<Double>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_grade);
        btnAdd = findViewById(R.id.btnAdd);
        txtGrade = findViewById(R.id.grade);
        btnSummary = findViewById(R.id.btnsummary);
        btnAdd.setOnClickListener(new View.OnClickListener() {

                                      @Override
                                      public void onClick(View v) {
                                          stgrade = txtGrade.getText().toString();
                                          if (stgrade.isEmpty()) {
                                              Toast.makeText(gradeActivity.this, "Please enter a grade", Toast.LENGTH_LONG).show();
                                          } else if (listOfGrades.contains(Double.parseDouble(stgrade))) {
                                              Toast.makeText(gradeActivity.this, "This grade already exist", Toast.LENGTH_LONG).show();
                                          } else {
                                              listOfGrades.add(Double.parseDouble(stgrade));
                                              txtGrade.setText("");
                                          }
                                      }
                                  });

        btnSummary.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent =new Intent(getApplicationContext(),summary_gradeActivity.class);
                startActivity(intent);
                Toast toast =Toast.makeText(getApplicationContext(),"This button has been clicked",Toast.LENGTH_LONG);
                        toast.show();
            }
        });
    }

}
//main
package com.example.supi.testapplication;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;


public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
//pageone
package com.example.supi.testapplication;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class PageOneActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_page_one);
    }
}
//summary grade
package com.example.supi.testapplication;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.EditText;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.Locale;

public class summary_gradeActivity extends AppCompatActivity {
    EditText totalG;
    EditText averageG;
    EditText LowerG;
    EditText HigherG;
    Double totalg, averageg, lowestg, higherg;
    public ArrayList<Double> studentGrades;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_summary_grade);
        totalG = findViewById(R.id.total);
        averageG = findViewById(R.id.average);
        LowerG =findViewById(R.id.lower);
        HigherG = findViewById(R.id.higher);
        if (gradeActivity.listOfGrades.size() <= 0){
            Toast.makeText(summary_gradeActivity.this, "No grade values", Toast.LENGTH_LONG).show();
        } else {
            studentGrades = gradeActivity.listOfGrades;
        }
        totalg = getTotal();
        totalG.setText(Double.toString(totalg));
        averageg = getAverage();

        averageG.setText(Double.toString(averageg));
        lowestg = getAverage();
        LowerG.setText(Double.toString(lowestg));
        higherg = getHigher(studentGrades.get(0));
        HigherG.setText(Double.toString(higherg));

    }
    // Method to return the total grade
    private double getTotal() {
        double total = 0;
        for (int i = 0; i < studentGrades.size();
             i++) {
            total += studentGrades.get(i);
        }
        return total;
    }
    // Method to return the average
    public double getAverage() {
        double average = 0;
        average = totalg / studentGrades.size();
        return average;
    }
    // Method to return the lowest grade
    public double getLowest() {
        double lower = studentGrades.get(0);
        for (int i = 0; i < studentGrades.size();
             i++) {
            if (lower > studentGrades.get(i)){
                lower = studentGrades.get(i);
            }}
             return lower;
        }
           // method to return average

    public Double getAverageg() {
        double average = 0;
        average = totalg / studentGrades.size();
        return averageg;

    }
        // Method to return the higher grade
        public double getHigher(double firstValue){
            double high = firstValue;
            for (int i = 0; i < studentGrades.size();
                 i++) {
                if (high < studentGrades.get(i)) {
                    high = studentGrades.get(i);
                }
            }
            return high;
        }
    }
    





