import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gerenciador de Contatos',
      home: Scaffold(
        appBar: AppBar(title: const Text('Informações do Cliente')),
        body: PersonCard(
          person: Person(
            imagePath: 'assets/levi.png',
            name: 'Levi',
            lastName: 'Ackerman',
            number: '55881321354',
            cpf: '123.456.789-00',
            birthday: DateTime(1846, 2, 10),
            registeredAt: DateTime.now(),
          ),
        ),
      ),
    );
  }
}

class Person {
  String imagePath;
  String name;
  String lastName;
  String number;
  String cpf;
  DateTime birthday;
  DateTime registeredAt;

  Person({
    required this.imagePath,
    required this.name,
    required this.lastName,
    required this.number,
    required this.cpf,
    required this.birthday,
    required this.registeredAt,
  });
}

class PersonCard extends StatelessWidget {
  final Person person;

  const PersonCard({super.key, required this.person});

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: const EdgeInsets.all(16),
      elevation: 8,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            CircleAvatar(
              radius: 50,
              backgroundImage: AssetImage(person.imagePath),
            ),
            const SizedBox(height: 16),
            Text('${person.name} ${person.lastName}', style: const TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
            const SizedBox(height: 8),
            InfoRow(label: 'Telefone', value: person.number),
            InfoRow(label: 'CPF', value: person.cpf),
            InfoRow(label: 'Nascimento', value: '${person.birthday.day}/${person.birthday.month}/${person.birthday.year}'),
            InfoRow(label: 'Registrado em', value: '${person.registeredAt.day}/${person.registeredAt.month}/${person.registeredAt.year}'),
          ],
        ),
      ),
    );
  }
}

class InfoRow extends StatelessWidget {
  final String label;
  final String value;

  const InfoRow({super.key, required this.label, required this.value});

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 4),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          Text('$label:', style: const TextStyle(fontWeight: FontWeight.bold)),
          Text(value),
        ],
      ),
    );
  }
}
