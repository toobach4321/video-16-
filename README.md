import 'package:flutter/material.dart';
import 'bmi_result_screen.dart'; // import result screen

class BMICalculatorScreen extends StatefulWidget {
  @override
  _BMICalculatorScreenState createState() => _BMICalculatorScreenState();
}

class _BMICalculatorScreenState extends State<BMICalculatorScreen> {
  double height = 160;
  double weight = 60;

  void _calculateAndNavigate() {
    final heightInMeters = height / 100;
    final bmi = weight / (heightInMeters * heightInMeters);

    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => BMIResultScreen(bmi: bmi),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('BMI Input')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            Text('Height: ${height.toStringAsFixed(1)} cm'),
            Slider(
              value: height,
              min: 100,
              max: 220,
              onChanged: (val) => setState(() => height = val),
            ),
            Text('Weight: ${weight.toStringAsFixed(1)} kg'),
            Slider(
              value: weight,
              min: 30,
              max: 150,
              onChanged: (val) => setState(() => weight = val),
            ),
            ElevatedButton(
              onPressed: _calculateAndNavigate,
              child: Text('Calculate BMI'),
            ),
          ],
        ),
      ),
    );
  }
}
import 'package:flutter/material.dart';

class BMIResultScreen extends StatelessWidget {
  final double bmi;

  BMIResultScreen({required this.bmi});

  String getBMICategory(double bmi) {
    if (bmi < 18.5) return "Underweight";
    if (bmi < 24.9) return "Normal";
    if (bmi < 29.9) return "Overweight";
    return "Obese";
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('BMI Result')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Your BMI is ${bmi.toStringAsFixed(1)}',
                style: TextStyle(fontSize: 26, fontWeight: FontWeight.bold)),
            Text('Category: ${getBMICategory(bmi)}',
                style: TextStyle(fontSize: 20)),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => Navigator.pop(context),
              child: Text('Back'),
            ),
          ],
        ),
      ),
    );
  }
}
