# Facebook Friends/Objects Rating

### Run the following script within your web browser's console while on Faebook.com


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

Notice the score moves in ascending order while you move down the list.  I had ~200 friends below a 0.47 rating (it looks like people I message are most are the highest).  Then I see a list of groups I below to, as well as groups I recognize and other I don't but can assume they are related to me through one of my existing likes/follows/clicks.

I then see my remaining friends, although they all have the same value '0.48703849209005'.  I then see a list of objects (local cities, local businesses, local schools, misc. words from my profile.

**What does your look like?**
