package com.example.clickgame

import android.os.Bundle
import android.os.CountDownTimer
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private var score = 0
    private lateinit var scoreTextView: TextView
    private lateinit var timeTextView: TextView
    private lateinit var clickButton: Button
    private lateinit var timer: CountDownTimer
    private var isGameStarted = false
    private val totalTime = 60000L  // 60秒
    private val interval = 1000L    // 每秒更新

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        scoreTextView = findViewById(R.id.score_text)
        timeTextView = findViewById(R.id.time_text)
        clickButton = findViewById(R.id.click_button)

        clickButton.setOnClickListener {
            if (!isGameStarted) {
                startGame()
            }
            score++
            scoreTextView.text = "得分: $score"
        }
    }

    private fun startGame() {
        isGameStarted = true
        timer = object : CountDownTimer(totalTime, interval) {
            override fun onTick(millisUntilFinished: Long) {
                timeTextView.text = "剩余时间: ${millisUntilFinished / 1000}秒"
            }

            override fun onFinish() {
                timeTextView.text = "游戏结束!"
                clickButton.isEnabled = false
            }
        }.start()
    }
}
