---
layout: post
title:  "How to improve your CSV / TSV workflow"
date:   2017-03-13 22:00:00 +0200
categories: csv tsv workflow game development spreadsheet
---
This blog post contains tips that you can use to improve your [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) / [TSV](https://en.wikipedia.org/wiki/Tab-separated_values) workflow. Terms CSV and TSV are also explained.

## Introduction to CSV / TSV workflow
If you haven't heard terms CSV or TSV earlier, do not worry. CSV is short for comma-separated values and TSV is short for tab-separated values. Basically both of them describe textual file formats where values are separated either with commas (CSV) or with tabs (TSV).

```
,Unit,Hitpoints,Armor,Movement speed,Damage,Attacks per second,DPS
,Swordman,100,10,1.00,10,1.00,10
,Brute,150,2,0.70,20,0.70,14
,Scout,60,3,1.30,5,1.20,6
,Archer,50,2,0.80,12,0.50,6
```
(CSV sample file)

&nbsp;

```
	Unit	Hitpoints	Armor	Movement speed	Damage	Attacks per second	DPS
	Swordman	100	10	1.00	10	1.00	10
	Brute	150	2	0.70	20	0.70	14
	Scout	60	3	1.30	5	1.20	6
	Archer	50	2	0.80	12	0.50	6
```
(TSV sample file)

&nbsp;

Then you might wonder why should you care about CSV or TSV. Well, the answer is simple: most spreadsheet programs (**Microsoft Excel**, **LibreOffice Calc**, **Google Docs** etc.) can output their current content as CSV or TSV files.

And at this point you should hear voices singing *"Hello Darkness, My Old Friend"* as you figure out that your [old enemy](https://xkcd.com/1667/) (always hated spreadsheet program) could be your best friend while you are developing a game.

Basically the whole process is following:

1. Add CSV or TSV parsing support to your game engine
2. Create or edit a spreadsheet in your (least) favourite spreadsheet program
3. Export that spreadsheet to CSV or TSV file
4. Read the CSV or TSV file in your game engine and use those values in game or generate new code from those values
5. Figure out what part of your game needs changes and jump back to step 2.

Now you might be wondering: 
*"Why should I use spreadsheet program instead of my own solution / JSON files / hard coded values / $1 ?"*, 
and answer is that almost anyone can use spreadsheet program, and with those new shiny online tools (like [Google Docs](https://docs.google.com/) and [Excel Online](https://office.live.com/)) you can easily add collaboration support to your game development process that is far more powerful than most homegrown tools. 

e.g. Google Docs supports simultaneously edits from multiple people, you get version history and you can directly download the spreadsheet as CSV or TSV file with any HTTP download tool.

&nbsp;

### Steps in your workflow that you can improve

There are lots of improvements you can do while working with this kind setup since CSV / TSV workflow can contain multiple steps:

#### Formatting

Some people want to keep their spreadsheets simple. Others want to add colors and formatting. The thing to remember in here is that only actual values are written to CSV / TSV files. So you can use formulas, colors, bolding, notes etc. to make your spreadsheet more (or less) useable and it won't have a negative effect to CSV / TSV files. 

Below are three formattings from same data (you can find the [actual spreadsheet](https://docs.google.com/spreadsheets/d/13Y94TU1uy9UgcN59MMxFDDvgbaxLX6kT_Zxe0ypL1CA/edit?usp=sharing) from Google Docs)

![Plain spreadsheet]({{ site.url }}/images/csv_unit_basic.png)
(plain)

&nbsp;

![Simple formatting spreadsheet]({{ site.url }}/images/csv_unit_formatted.png)
(simple formatting)

&nbsp;

![Colors and symbols spreadsheet]({{ site.url }}/images/csv_unit_colors_and_symbols.png)
(with colors and symbols)

&nbsp;

As you can see, the same data can be presented in many different ways. The thing to remember in here is that only the first sheet will be converted to CSV / TSV file. So you can easily add e.g. graphs, additional notes or images to those extra sheet and they won't bother the CSV / TSV generation at all.

If you want to use Unicode symbols (e.g. Emojis like 🛡) in your CSV / TSV files, make sure your text file parsers also supports those. And also inform other collaborators about what kind of things you are allowed to use.

&nbsp;

#### Functions

There are many useful functions that you can use while creating your spreadheet files. I have listed some useful ones below, and you can check out their usage examples from [this spreadsheet](https://docs.google.com/spreadsheets/d/1_zIOuq_ez4AbVWED1lLJrtLEysYArdPwc7OyIo-Ri0A/edit?usp=sharing)

* **NOW()**, is used to display last edit time of the document. Very useful since one can easily check from CSV / TSV file when last edit for spreadsheet file was done.
* **SUBSTITUTE()**, is used to replace existing text with new text in a string. This is useful for localization spreadsheets where text examples with replace might be needed
* **ROUND()**, is used to round decimal numbers
* **SUM()**, is used to sum values from different cells together
* **IF()**, does conditional output based on comparision

![Useful functions spreadsheet]({{ site.url }}/images/csv_functions_sample.png)

&nbsp;

#### Validation

Since it is easy to add invalid values to spreadsheet (e.g. copy+paste error turns 100 to 10t0), you might want to add additional validations to your workflow. Easiest thing is to add validations directly to spreadsheet (e.g. number in this cell must be between 1 and 100) but you might want to use additional validation in your code, specially if invalid values can cause crashes or other nasty experiences for users.

If you use separate code for validating, then here are few tips you can do:

1. Check that every line has equal number of commas (CSV) or tabs (TSV), assuming that actual elements do NOT contain extra commas or tabs
2. You might want to skip lines that only contain commas (CSV) or tabs (TSV)
3. Be VERY strict about input and error out immediately if something does not match your requirements. (e.g. in C# programming language [Enum.Parse](https://msdn.microsoft.com/en-us/library/essfb559(v=vs.110).aspx) function accepts numbers, and this could lead to an issue, if you only want to accept enums)

&nbsp;

#### Code generation

You can extend your CSV / TSV workflow to include code generation. This is not viable method on all platforms, but if you don't want or need runtime CSV / TSV parsing in your game then this is one way to use power of CSV / TSV file.

If we use the CSV file from beginning of this post, we can use following C# code to generate static readonly dictionary that contains those values.

{% highlight csharp %}
using System;
using System.Text;
using System.IO;
					
public class Program
{
	public enum UnitType 
	{
		Swordman,
		Brute,
		Scout,
		Archer
	}
	
	public class UnitStats
	{
		public int hitpoints;
		public int armor;
		public float movement;
		public int damage;
		public float attacksPerSecond;
		public float damagePerSecond;
		
		public UnitStats(int hp, int arm, float mov, int dama, float aps, float dps)
		{
			this.hitpoints = hp;
			this.armor = arm;
			this.movement = mov;
			this.damage = dama;
			this.attacksPerSecond = aps;
			this.damagePerSecond = dps;
		}
	}
	
	
	public static void Main()
	{
		string csvInput = @",Unit,Hitpoints,Armor,Movement speed,Damage,Attacks per second,DPS
                            ,Swordman,100,10,1.00,10,1.00,10
                            ,Brute,150,2,0.70,20,0.70,14
                            ,Scout,60,3,1.30,5,1.20,6
                            ,Archer,50,2,0.80,12,0.50,6";
		
		StringBuilder builder = new StringBuilder();
		
		builder.AppendLine("private readonly Dictionary<UnitType,UnitStats> unitValues = new Dictionary<UnitType,UnitStats>()");
		builder.AppendLine("{");
		
		using (StringReader reader = new StringReader(csvInput))
		{
			// Loop over the lines in the string.
			string line;
			
			UnitType unitType;
			
			while ((line = reader.ReadLine()) != null)
			{
				string[] splitted = line.Split(',');
				
				// Only process entries that start with proper enum
				if (splitted.Length > 1 && Enum.TryParse(splitted[1], out unitType))
				{
					builder.Append("   { UnitType." + splitted[1] + ", new UnitStats(");
					for (int j = 2; j < splitted.Length; j++)
					{
						builder.Append(splitted[j]);
						
						// Add f for floats
						if (splitted[j].Contains("."))
						{
							builder.Append("f");
						}
						
                        // Add commas when needed
						if (j != splitted.Length - 1)
						{
							builder.Append(", ");
						}
					}
					builder.AppendLine(") },");
				}
			}
		}

		builder.AppendLine("};");
		
		Console.Write(builder.ToString());
	}
}
{% endhighlight %}

and output will be

{% highlight csharp %}
private readonly Dictionary<UnitType,UnitStats> unitValues = new Dictionary<UnitType,UnitStats>()
{
   { UnitType.Swordman, new UnitStats(100, 10, 1.00f, 10, 1.00f, 10) },
   { UnitType.Brute, new UnitStats(150, 2, 0.70f, 20, 0.70f, 14) },
   { UnitType.Scout, new UnitStats(60, 3, 1.30f, 5, 1.20f, 6) },
   { UnitType.Archer, new UnitStats(50, 2, 0.80f, 12, 0.50f, 6) },
};
{% endhighlight %}

&nbsp;

#### Optimization
If you only have few entries (cells with values) in your CSV / TSV file, then you shouldn't really worry about the parsing performance. But if you have hundreds or even thousand entries in your CSV / TSV file then you should spend a bit of time to make CSV / TSV handling more efficient. 

The parsing method I suggest is to read those CSV / TSV entries line by line and splitting each line separately. After the splitting you can feed those values forward e.g. to your constructors.

Some people like to use [Regex](https://en.wikipedia.org/wiki/Regular_expression) for splitting, but I would avoid it with CSV / TSV files since Regex is a bit of overkill for that purpose. In most cases it is easier to rely on [KISS principle](https://en.wikipedia.org/wiki/KISS_principle) and not to construct too complicated CSV / TSV entries.

&nbsp;

In certain situations you can get massive performance improvements if you generate optimized CSV / TSV files from the originals. Things you can optimize in cases like these are:

* enums (**UnitType.Archer** becomes **1**), which are faster to cast from number to chosen enum type than parsing the enum type from string 
* booleans (**true** becomes **1**)
* durations (**1min 40seconds** becomes **100**), which can be expressed e.g. as seconds 
* color values (RGB Hex **#78FF25** becomes **7929637**)

below you can see snippets from original CSV file and "optimized" CSV file

```
Unit type, Is ground unit, Training time, Unit selection color, Bonus damage type, Speed
Archer, true, 1 min, 255 255 0, Fire, 13
```

 ▼ 

```
Unit type, Is ground unit, Training time, Unit selection color, Bonus damage type, Speed
3, 1, 60, 16776960, 2, 13
```

&nbsp;

With massive CSV / TSV files, you should target for sparse presentation. That means you should set base/default value and only populate the entries if they are different than base/default value. This makes parsing a bit faster and saves some storage space.

Below are [examples](https://docs.google.com/spreadsheets/d/1PTqUD58UWJVy3u8z7y5tX-XsXRwu4jH_4fSbdsw2Aqw/pubhtml) from sparse vs. dense

![Sparse vs. dense spreadsheet]({{ site.url }}/images/csv_sparse_vs_dense.png)
(empty cells in sparse are highlighted with pink color)

&nbsp;

#### Dots vs. commas with decimal numbers
If you are going to use decimal numbers in your CSV / TSV files, make sure you use either dots or commas as [decimal separators](https://simple.wikipedia.org/wiki/Decimal_separator). Do not mix and match since it only confuses people.

Also make sure you set your CSV / TSV parsing locale to match your selection. Otherwise you might end situation where the parsing doesn't work in all environments or produces incorrect results.

&nbsp;

### Examples

I have already given few examples in this post, but here are additional ones that might inspire you

[Game map](https://docs.google.com/spreadsheets/d/1iu3APNmzJO-uRZdmNVzRp49PyDd4gcJ5iZpfJTnTQFY/edit?usp=sharing)
![Game map spreadsheet]({{ site.url }}/images/csv_map_cells.png)

[Medal times](https://docs.google.com/spreadsheets/d/1uZLF3JT86n5QwcFAWzX3UH8RL2u34vv1WGlv_lQFp4U/edit?usp=sharing)
![Medal times spreadsheet]({{ site.url }}/images/csv_medal_times.png)

[Shop values](https://docs.google.com/spreadsheets/d/1dJl6JIQzEaMIuV0KfCNf5ITQfdsk64_tMqPrYMvfFus/edit?usp=sharing)
![Shop values spreadsheet]({{ site.url }}/images/csv_shop_values.png)