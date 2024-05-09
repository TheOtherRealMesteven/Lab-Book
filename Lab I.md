# Final Lab - Lab I

## Lab Results
*For review, the results of the lab has been submitted below.*

### Times created by VM
| Command | Times 1 | Times 2 | Times 3 | Times 4 | Average |
|---------|---------|---------|---------|---------|---------|
|BuildNetwork|949|963|964|977|**963**|
|MaxDist|20|20|34|20|**23**|
|MaxLink|4|2|5|2|**3**|
|FindDist 9361783 11391765|52|56|60|56|**56**|
|FindNeighbour 8611522|15|19|18|17|**17**|
|Check Rail 14601225 12321385 8611522 9361783|22|42|28|23|**28**|
|Check Ship 14601225 12321385 8611522 9361783|16|24|24|18|**20**|
|FindRoute Rail 9081958 15832241|23|29|25|23|**25**|
|FindRoute Ship 9081958 15832241|18|13|15|15|**15**|
|FindShortestRoute Rail 9081958 15832241|25|25|26|22|**25**|
|FindShortestRoute Ship 9081958 15832241|11|18|12|10|**13**|

Overall, the timings were similar to what I had expected on my personal machine, the build network time was suprising however, as my values rarely reached the triple digits. But, here it did so consistently.

My main concern was with my switch statements decreasing the reliability of my time results, they made the program marginally faster, but made the results vary from low 20 microseconds up to 100 microseconds.

### Output.txt
```
MaxDist
Malton Rail,Zeebrugge Harbour,411.279

MaxLink
51889340,17191741,356.309

FindDist 9361783 11391765
Selby Rail,Howden Rail,13.531

FindNeighbour 8611522
8631524
11251704
9361783
12321385
13491586

Check Rail 14601225 12321385 8611522 9361783 
14601225,12321385,PASS
12321385,8611522,PASS
8611522,9361783,PASS

Check Ship 14601225 12321385 8611522 9361783 
14601225,12321385,FAIL

FindRoute Rail 9081958 15832241
9081958
12032132
15832241

FindRoute Ship 9081958 15832241
FAIL

FindShortestRoute Rail 9081958 15832241
9081958
12032132
15832241

FindShortestRoute Ship 9081958 15832241
FAIL


```

Based on the sample outputs we were given that correspond to the sample commands, I believe my code is accurate to the output format and result expectation.

### Parasoft Report
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/92726c94-7557-47ed-8839-605923c0ce92)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/f8537843-235a-4c24-962f-211313394b58)

The two severity three ratings are in the `Main.cpp` file and as such were not rectified as we were not permitted to modify the `Main.cpp` file.

## Lab Review
*A breakdown or review of the lab has been listed below.*

<details>
  <summary>Implementation Details</summary>

  <details>
    <summary>Process Command</summary>

For the implementation of the commands, I used a switch statement in combination to an unordered map. If this were programmed in c# the unordered map would not be necessary but with c++ switch statements cannot operate with strings as the switch condition and thus I had to convert the strings inputs into a numerical value to switch with and the most efficient solution was to use an unordered map.
```c++
enum class Command {
	MaxDist,
	MaxLink,
	FindDist,
	FindNeighbour,
	Check,
	FindRoute,
	FindShortestRoute
};

std::unordered_map<std::string, Command> commandMap = {
		{"MaxDist", Command::MaxDist},
		{"MaxLink", Command::MaxLink},
		{"FindDist", Command::FindDist},
		{"FindNeighbour", Command::FindNeighbour},
		{"Check", Command::Check},
		{"FindRoute", Command::FindRoute},
		{"FindShortestRoute", Command::FindShortestRoute}
};

bool Navigation::ProcessCommand(const std::string& commandString) {
	std::istringstream inString(commandString);
	std::string command;
	inString >> command;

	Network& network = Network::getInstance();
	const auto it = commandMap.find(command);
	if (it == commandMap.end()) return false;
	switch (it->second)
	{
	case Command::MaxDist:
	{
		network.getMaxDist(_outFile);
		return true;
	}
	case Command::MaxLink:
	...
}
```

As for the commands parameters, I primarily just used right-shift operators to assign them directly.
```c++
case Command::FindShortestRoute:
{
	std::string mode;
	int input3, input4;
	inString >> mode >> input3 >> input4;
...
```

  </details>
</details>
