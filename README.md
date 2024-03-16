# Be-Healthy
this is my first project using Flutter

import 'dart:js';
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

import 'package:untitled/about_us.dart';
import 'package:untitled/home.dart';
import 'package:untitled/chat.dart';
import 'package:untitled/near.dart';
import 'package:untitled/settings.dart';
import 'package:untitled/coaches.dart';
import 'package:untitled/exercises.dart';
import 'package:untitled/profile.dart';
import 'my_drawer_header.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  var currentPage = DrawerSections.settings;

  @override
  Widget build(BuildContext context) {
    var container;

    if (currentPage == DrawerSections.home) {
      container = MyHomePage();
    } else if (currentPage == DrawerSections.profile) {
      container = ProfilePage(
        personalPhoto: '',
        backgroundPhoto: '',
        name: 'Mahmoud Efat',
        username: '@mahmoud24',
        country: '',
        age: 24,
      );
    } else if (currentPage == DrawerSections.chat) {
      container = MessagesPage();
    } else if (currentPage == DrawerSections.coaches) {
      container = CoachesPage();
    } else if (currentPage == DrawerSections.near) {
      container = NearPage();
    } else if (currentPage == DrawerSections.exercises) {
      container = ExercisesPage();
    } else if (currentPage == DrawerSections.about_us) {
      container = InformationPage();
    } else if (currentPage == DrawerSections.settings) {
      container = SettingsPage();
    }

    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.blueAccent,
        centerTitle: true,
        title: const Text("Be Helthy"),
      ),
      body: container,
      drawer: Drawer(
        child: SingleChildScrollView(
          child: Container(
            child: Column(
              children: [
                MyHeaderDrawer(),
                MyDrawerList(context),
              ],
            ),
          ),
        ),
      ),
    );
  }

  //shows the list of menu drawer
  Widget MyDrawerList(context) {
    return Container(
      padding: const EdgeInsets.only(top: 15),
      child: Column(
        children: [
          menuItem(context, 1, "Home", Icons.home,
              currentPage == DrawerSections.home ? true : false),
          menuItem(context, 2, "Profile", Icons.person,
              currentPage == DrawerSections.profile ? true : false),
          menuItem(context, 3, "Messages", Icons.message,
              currentPage == DrawerSections.chat ? true : false),
          menuItem(context, 4, "Coaches", Icons.person_2_outlined,
              currentPage == DrawerSections.coaches ? true : false),
          menuItem(context, 5, "Near", Icons.location_on,
              currentPage == DrawerSections.near ? true : false),
          menuItem(context, 6, "Exercises", Icons.sports_gymnastics,
              currentPage == DrawerSections.exercises ? true : false),
          menuItem(context, 7, "About us", Icons.question_mark,
              currentPage == DrawerSections.about_us ? true : false),
          const Divider(),
          menuItem(context, 8, "Settings", Icons.settings,
              currentPage == DrawerSections.settings ? true : false),
        ],
      ),
    );
  }

  Widget menuItem(BuildContext context, int id, String title, IconData icon,
      bool selected) {
    return Material(
      color: selected ? Colors.grey : Colors.transparent,
      child: InkWell(
        onTap: () {
          Navigator.pop(context);

          setState(() {
            if (id == 1) {
              currentPage = DrawerSections.home;
            } else if (id == 2) {
              currentPage = DrawerSections.profile;
            } else if (id == 3) {
              currentPage = DrawerSections.chat;
            } else if (id == 4) {
              currentPage = DrawerSections.coaches;
            } else if (id == 5) {
              currentPage = DrawerSections.near;
            } else if (id == 6) {
              currentPage = DrawerSections.exercises;
            } else if (id == 7) {
              currentPage = DrawerSections.about_us;
            } else if (id == 8) {
              currentPage = DrawerSections.settings;
            }
          });
        },
        child: Padding(
          padding: const EdgeInsets.all(15.5),
          child: Row(
            children: [
              Expanded(
                child: Icon(
                  icon,
                  size: 20,
                  color: Colors.black,
                ),
              ),
              Expanded(
                flex: 3,
                child: Text(
                  title,
                  style: const TextStyle(
                    color: Colors.black,
                    fontSize: 16,
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

enum DrawerSections {
  home,
  profile,
  chat,
  coaches,
  near,
  exercises,
  about_us,
  settings,
}
