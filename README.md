package com.electricalguru

import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
import com.electricalguru.utils.OhmsLawCalculator

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val etVoltage = findViewById<EditText>(R.id.etVoltage)
        val etCurrent = findViewById<EditText>(R.id.etCurrent)
        val btnCalculate = findViewById<Button>(R.id.btnCalculate)
        val tvResult = findViewById<TextView>(R.id.tvResult)

        btnCalculate.setOnClickListener {
            val voltage = etVoltage.text.toString().toDoubleOrNull()
            val current = etCurrent.text.toString().toDoubleOrNull()

            if (voltage != null && current != null) {
                val resistance = OhmsLawCalculator.calculateResistance(voltage, current)
                val power = OhmsLawCalculator.calculatePower(voltage, current)
                tvResult.text = "Resistance: %.2f Ω\nPower: %.2f W".format(resistance, power)
            } else {
                tvResult.text = "Please enter valid Voltage and Current values."
            }
        }
    }
}
