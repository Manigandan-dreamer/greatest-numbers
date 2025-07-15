import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: GreatestApp()));

class GreatestApp extends StatefulWidget {
  @override
  _GreatestAppState createState() => _GreatestAppState();
}

class _GreatestAppState extends State<GreatestApp> {
  final n1 = TextEditingController();
  final n2 = TextEditingController();
  final n3 = TextEditingController();
  String result = '';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Greatest of Three'),
        backgroundColor: Colors.teal,
      ),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Column(
          children: [
            TextField(
              controller: n1,
              decoration: InputDecoration(labelText: 'Enter First Number'),
              keyboardType: TextInputType.number,
            ),
            TextField(
              controller: n2,
              decoration: InputDecoration(labelText: 'Enter Second Number'),
              keyboardType: TextInputType.number,
            ),
            TextField(
              controller: n3,
              decoration: InputDecoration(labelText: 'Enter Third Number'),
              keyboardType: TextInputType.number,
            ),
            SizedBox(height: 15),
            ElevatedButton(
              style: ElevatedButton.styleFrom(backgroundColor: Colors.teal),
              onPressed: () {
                int a = int.tryParse(n1.text) ?? 0;
                int b = int.tryParse(n2.text) ?? 0;
                int c = int.tryParse(n3.text) ?? 0;
                setState(() {
                  result = 'Greatest is: ${[a, b, c].reduce((x, y) => x > y ? x : y)}';
                });
              },
              child: Text('Find Greatest'),
            ),
            SizedBox(height: 15),
            Text(
              result,
              style: TextStyle(fontSize: 18, color: Colors.teal),
            ),
          ],
        ),
      ),
    );
  }
}
