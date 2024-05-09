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

For this project, I primarily handled my code with a new class `Network`. This class would handle all the processes relating to the network of node and arcs which is the entirety of the project. Its was mainly used this way as the class managed the unordered_map containing all the nodes and the vector list of the arcs, which made referencing far easier than if I had seperated the methods.

There were additional files for Node and Arcs classes so they could be setup as objects to be used later on, but these primarily held information related to creating the class and retrieving the encapsulated information they held.

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
<details>
	<summary>Build Network</summary>

For build network, I have two while loops which iterate through each line in each file. Initially, they were both reading the files using stringstream methods.
```c++
		std::string name;
		int referenceId;
		double latitude, longitude;

		std::getline(iss, name, ',');
		iss >> referenceId;
		iss.ignore();
		iss >> latitude;
		iss.ignore();
		iss >> longitude;
```
However, this was replaced later on which reduced 1000 microseconds off of the build network time, making it drastically faster. (I know that build network will not be marked, but small numbers are good for time values)
```c++
		size_t pos1 = line.find(',');
		size_t pos2 = line.find(',', pos1 + 1);
		size_t pos3 = line.find(',', pos2 + 1);
		std::string name = line.substr(0, pos1);
		int referenceId = std::stoi(line.substr(pos1 + 1, pos2 - pos1 - 1));
		double latitude = std::stod(line.substr(pos2 + 1, pos3 - pos2 - 1));
		double longitude = std::stod(line.substr(pos3 + 1));
```
The code above shows the current method, rather than using the ignore method and right shifting, we use string manipulation to find the parameters and pass them to their numerical forms.


In addition to this, as `MaxDist` and `MaxLink` require no inputs, they can be calculated in the build network method as it would be a minimal addition to the calculation speed.
### Max Link
Max link was far easier than MaxDist, you will findout why in a moment, as it only required an additional if statement on the end of the original iteration code.
```c++
if (!CachedLongestArc || newArc->getDistance() > CachedLongestArc->getDistance()) {
	CachedLongestArc = newArc;
}
```
And then it could be stored as an outputstream to ensure minimal processing is done when it came to the timed execution of the method.
```c++
void processMaxLink(const Arc* CachedLongestArc) {
	m_MaxLink << "MaxLink" << "\n" << CachedLongestArc->getStartNode()->getReferenceNumber() << "," << CachedLongestArc->getEndNode()->getReferenceNumber() << "," << std::fixed << std::setprecision(3) << CachedLongestArc->getDistance() / 1000 << "\n\n";
}
```

### Max Dist
Max distance was originally extremely inefficient. At the start, it was executed after build network was complete and due to its nested for loops, it forced the build network time into quadruple digits.
```c++
        for (const auto& nodePair : nodes) {
            for (const auto& nodePair2 : nodes) {
                if (nodePair.first != nodePair2.first) {
                    double x1, y1, x2, y2;
                    Utility::LLtoUTM(nodePair.second->getLatitude(), nodePair.second->getLongitude(), x1, y1);
                    Utility::LLtoUTM(nodePair2.second->getLatitude(), nodePair2.second->getLongitude(), x2, y2);
                    double distance = pow(x2 - x1, 2) + pow(y2 - y1, 2);
                    if (distance > maxDistance) {
                        maxDistance = distance;
                        furthestStartNode = nodePair.second;
                        furthestEndNode = nodePair2.second;
                    }
                }
```
The second iteration was able to reduce the processing time down to triple digits, around the 3000 micro second mark by removing the initial for loop and instead merging it with the while loop which was already inplace.
```c++
		iss >> latitude;
		iss.ignore();
		iss >> longitude;
		Node* newNode = new Node(referenceId, name, latitude, longitude);
		Network::network.addNode(newNode);

		// Calculate Max Dist
		std::unordered_map<int, Node*>& Map = Network::network.getNodeMap();
		for (const auto& nodePair2 : Map) {
			if (referenceId != nodePair2.first) {
				double x1, y1, x2, y2;
				Utility::LLtoUTM(latitude, longitude, x1, y1);
				Utility::LLtoUTM(nodePair2.second->getLatitude(), nodePair2.second->getLongitude(), x2, y2);
				double distance = pow(x2 - x1, 2) + pow(y2 - y1, 2);
				if (distance > maxDistance) {
					maxDistance = distance;
					bestEnd = name;
					bestStart = nodePair2.second->getName();
				}
			...
```
The issue with the second iteration was the two method calls ran with each node in a nested for loop. Having a large amount of nodes made this increment the time value by a large amount.
To fix this issue, the third iteration reworked the node class to store the latitude and longitude values **after** they had been processed by the method as where it was called in the program, the method was also called to convert the values. So it was logical to simplify the process.
```c++
Node* const newNode = new Node(referenceId, name, x, y);
network.addNode(newNode);

// Calculate Max Dist
const std::unordered_map<int, Node*>& Map = network.getNodeMap();
for (const auto& nodePair2 : Map) {
	if (referenceId != nodePair2.first) {
		const double latDiff = x - nodePair2.second->getLatitude();
		const double longDiff = y - nodePair2.second->getLongitude();
		const double distanceSquared = latDiff * latDiff + longDiff * longDiff;
		if (distanceSquared > maxDistance) {
			maxDistance = distanceSquared;
			bestEnd = name;
			bestStart = nodePair2.second->getName();
		}
	...
```
This cut the processing time in half, resulting in around 1200 microseconds to complete the buildnetwork process.
</details>
<details>
	<summary>MaxDist and MaxLink</summary>

 MaxDist and MaxLink were both calculated in `BuildNetwork` then stored as an output string to be assigned to the output file.
 This meant that their times were drastically minimized when timed as it had been precalculated and cached.
```c++
case Command::MaxDist:
{
	network.getMaxDist(_outFile);
	return true;
}

const void getMaxLink(std::ostream& outputStream) const {
	outputStream << m_MaxLink.str();
}

const void getMaxDist(std::ostream& outputStream) const {
	outputStream << m_MaxDist.str();
}
```

</details>
<details>
	<summary>FindDist</summary>

FindDist was a simple process, using right shifting the parameters could be retrieved from the input string and then passed to a method which found the nodes, got their co-ordinates and returned the distance between them. Running the utility method to convert the co-ordinates when creating the nodes assisted here as there were no method calls aside from using getters to retrieve values, which are rather efficient themselves.
```c++
std::ostringstream findDist(int startRef, int endRef) const {
	Node* const startNode = findNode(startRef);
	Node* const endNode = findNode(endRef);

	const double latDiff = startNode->getLatitude() - endNode->getLatitude();
	const double longDiff = startNode->getLongitude() - endNode->getLongitude();
	const double distance = sqrt(latDiff * latDiff + longDiff * longDiff);

	std::ostringstream returnValue;
	returnValue << "FindDist " << startRef << " " << endRef << "\n" << startNode->getName() << "," << endNode->getName() << "," << std::fixed << std::setprecision(3) << distance / 1000 << "\n\n";
	return returnValue;
}
```

</details>
<details>
	<summary>FindNeighbour</summary>

FindNeighbour was also a simple process, once again right shifting allowed us to retrieve the node identifier and thus the node from the input.
From that, we could iterate through the arcs and return the ones which had either started or ended at the given node (Because the arcs are reversible).

```c++
std::ostringstream Network::listNeighbors(const Node* node) {
	std::ostringstream returnValue;
	for (const auto& arc : arcs) {
		if (arc->getStartNode() == node) {
			returnValue << arc->getEndNode()->getReferenceNumber() << "\n";
		}
		else if (arc->getEndNode() == node) {
			returnValue << arc->getStartNode()->getReferenceNumber() << "\n";
		}
	}
	return returnValue;
}
```

</details>
<details>
	<summary>Check</summary>
</details>
<details>
	<summary>FindRoute</summary>
</details>
</details>
