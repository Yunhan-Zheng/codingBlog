---
layout: post
title: Simple portfolio
tags: wayfair
---
<li>
<a><strong>TOC</strong></a>
</li>

* [Project Zyborg](#zyborg)
* [CRM for a Real Estate company](#realEstate)
* [Food Order System](#university)

<h3 id="zyborg">Project Zyborg</h3>

It is a 3D RPG game built with Unity using C#.

The sample below is the script for a menu where user can start/pause/quit the game by clicking corresponding buttons.

``` C#
using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class menuScript : MonoBehaviour {

	public Canvas quitMenu;
	public Button startText;
	public Button exitText;


	// Use this for initialization
	void Start () {
		quitMenu = quitMenu.GetComponent<Canvas> ();
		startText = startText.GetComponent<Button> ();
		exitText = exitText.GetComponent<Button> ();
		quitMenu.enabled = false;
	}
	
	// Show the quit menu
	public void ExitPress()
	{
		quitMenu.enabled = true;
		startText.enabled = false;
		exitText.enabled = false;
	}

	//Press buttton No
	public void NoPress()
	{
		quitMenu.enabled = false;
		startText.enabled = true;
		exitText.enabled = true;
	}

	public void StartLevel()
	{
		Application.LoadLevel (1);
	}

	public void ExitGame()
	{
		Application.Quit ();
	}
}
```

The sample below is the script for the Actor class which is a super class for player, enemy, NPC and projectile classes.
``` C#
using UnityEngine;
using System.Collections;

public class Actor : MonoBehaviour {

    public Stats _stats;

    private int _id;
    private string _name;

    public Actor()
    {
        _stats = new Stats();
    }

    /// <value>The identifier number for this object.</value>
    public int Id {
        get {
            return _id;
        }

        set {
            _id = value;
        }
    }

    public string Name {
        get {
            return _name;
        }

        set {
            _name = value;
        }
    }

    public Stats ActorStats {
        get {
            return _stats;
        }

        set {
            _stats = value;
        }
    }
}
```

<h3 id="realEstate">CRM for a Real Estate company</h3>

The below domain model is about a CRM system for a real estate company. It provides customer/employee access for property listings, preference editing, offer bidding and tracking, etc.

<a href="{{site.baseurl}}/public/image/Real estate company information system.png"><img alt="Domain model for a real estate company's information system" src="{{site.baseurl}}/public/image/Real estate company information system.png"/></a>

<h3 id="university">Food Order System</h3>

The below sequence digram depicts the interactions among customers, system, cafeteria and payment processor.
<a href="{{site.baseurl}}/public/image/Assignment 5-4.png"><img alt="Sequence diagram for a university cafeteria ordering system" src="{{site.baseurl}}/public/image/Assignment 5-4.png"/></a>