import 'package:flutter/material.dart';

void main() {
  runApp(const GreatestNumberApp());
}

class GreatestNumberApp extends StatelessWidget {
  const GreatestNumberApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Greatest of Three Numbers',
      theme: ThemeData(primarySwatch: Colors.deepPurple),
      home: const GreatestFinderScreen(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class GreatestFinderScreen extends StatefulWidget {
  const GreatestFinderScreen({super.key});

  @override
  State<GreatestFinderScreen> createState() => _GreatestFinderScreenState();
}

class _GreatestFinderScreenState extends State<GreatestFinderScreen> {
  final TextEditingController _num1Ctrl = TextEditingController();
  final TextEditingController _num2Ctrl = TextEditingController();
  final TextEditingController _num3Ctrl = TextEditingController();

  String _result = '';

  void _findGreatest() {
    final num1 = int.tryParse(_num1Ctrl.text);
    final num2 = int.tryParse(_num2Ctrl.text);
    final num3 = int.tryParse(_num3Ctrl.text);

    if (num1 == null || num2 == null || num3 == null) {
      setState(() {
        _result = '❌ Please enter valid numbers';
      });
      return;
    }

    int greatest = num1;
    if (num2 > greatest) greatest = num2;
    if (num3 > greatest) greatest = num3;

    setState(() {
      _result = '✅ Greatest number is: $greatest';
    });
  }

  void _reset() {
    _num1Ctrl.clear();
    _num2Ctrl.clear();
    _num3Ctrl.clear();
    setState(() {
      _result = '';
    });
  }

  Widget _buildNumberInput(String label, TextEditingController controller) {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 8),
      child: TextField(
        controller: controller,
        keyboardType: TextInputType.number,
        decoration: InputDecoration(
          labelText: label,
          border: OutlineInputBorder(borderRadius: BorderRadius.circular(10)),
        ),
      ),
    );
  }

  @override
  void dispose() {
    _num1Ctrl.dispose();
    _num2Ctrl.dispose();
    _num3Ctrl.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Find Greatest Number')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            _buildNumberInput('Enter Number 1', _num1Ctrl),
            _buildNumberInput('Enter Number 2', _num2Ctrl),
            _buildNumberInput('Enter Number 3', _num3Ctrl),
            const SizedBox(height: 20),
            Row(
              children: [
                Expanded(
                  child: ElevatedButton(
                    onPressed: _findGreatest,
                    child: const Text('Find Greatest'),
                  ),
                ),
                const SizedBox(width: 10),
                Expanded(
                  child: OutlinedButton(
                    onPressed: _reset,
                    child: const Text('Reset'),
                  ),
                ),
              ],
            ),
            const SizedBox(height: 20),
            if (_result.isNotEmpty)
              Card(
                color: Colors.deepPurple.shade50,
                elevation: 3,
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
                child: Padding(
                  padding: const EdgeInsets.all(16.0),
                  child: Text(
                    _result,
                    style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                  ),
                ),
              ),
          ],
        ),
      ),
    );
  }
}
