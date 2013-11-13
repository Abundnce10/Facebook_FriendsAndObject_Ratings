## Facebook Friends/Objects Rating

#### Run the following script within your web browser's console while on Faebook.com


```javascript
function creator(o, data, node){
	var content = document.createElement(node);
	var cell = document.createTextNode(data);
	content.appendChild(cell);
	o.appendChild(content);
}
function displayData(arr){
	var table = document.createElement('table');
	var thead = document.createElement('thead');
	table.appendChild(thead);
	var row = document.createElement('tr');
	creator(row, 'Name', 'th');
	creator(row, 'Score', 'th');
	thead.appendChild(row);
	var tbody = document.createElement('tbody');
	table.appendChild(tbody);
	for(i=0; i<arr.length; i++){
		var row = document.createElement('tr');
		creator(row, arr[i]["text"], 'td');
		creator(row, arr[i]["grammar_costs"]["{user}"], 'td');	
		tbody.appendChild(row);
	}
	document.body.innerHTML = "";
	document.body.appendChild(table);
}

id = requireDynamic("Env").user;
url = "//www.facebook.com/ajax/typeahead/search/facebar/bootstrap/?viewer=" + id + "&__a=1";
x = new XMLHttpRequest();
x.onreadystatechange=function(){
  if (x.readyState==4 && x .status==200){
    srr=JSON.parse(x.responseText.substring(9)).payload.entries;
    displayData(srr);
  }
}
x.open("GET",url,true);
x.send();
```

#### What does yours look like?

Notice how the scores move in ascending order as you scroll down the list.  I had ~200 friends below a 0.47 rating (at first glance it looks like mainly people I message the most).  After those friends I see a list of groups I belong to, as well as groups I recognize.  There are other groups I'm unaware of but can presume they are related to me through one of my existing: page likes, people follows, link clicks.

I then see my remaining friends, although they all have the same value '0.48703849209005'.  Following that I then see a list of objects (local cities, local businesses, local schools, misc. words from my profile).  The majority of my ratings for objects other than people are 'undefined'.

#### Credit

I'm intrigued by the amount of objects from which they're tracking myself against for correlation, but I wasn't aware of this ability until I stumbledup over [Arjun Shreedharan's blog](http://arjunsreedharan.org/).  In one of his [posts](http://arjunsreedharan.org/post/65979958297/find-your-facebook-friends-ranking-score) he presents the code above.

