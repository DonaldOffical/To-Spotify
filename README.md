# To-Spotify
Some information about how to sync NetEase Cloud Music playlists to your Spotify.

This note is aim to solve the problem about playlists across different music applications, such as QQ music and NetEase Cloud music. Take NetEase for an example. You can use the same way for your QQ music playlists too. 

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/logo.png)

Show respect to yueyericardo
```
https://github.com/yueyericardo/Netease-to-Youtube-or-Spotify
```
to bjason
```
https://github.com/bjason/163MusicToSpotify
```
to Binaryify
```
https://github.com/Binaryify/NeteaseCloudMusicApi
```

If you want to see the code, API or some other documents, please click the link above to vist these great releases. 
There is the eaeiest way to export your playlists in my opinion. (Thank to yueyericardo)

The first step is getting the id of your playists.
You can login NetEase Cloud Music on website, and open one of your playlist. Then you will see the playlist id on the address bar. 
like this:

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/%E7%BD%91%E6%98%93%E4%BA%91%E6%AD%8C%E5%8D%95.png)

cpoy the number after "id="
```
id="......."
```
Congratulations! Now you get your playist id!

The second step is use this id to get the name list of this playlist. 
Now you can visit yueyericardo's website. (Thanks again!)
```
https://yyrcd.com/2018/11/14/n2s-zh/
```
Paste your playlist id which you got from the first step here. 
like this:

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/API%201.png)

After this step, you will get your all songs' names and singers of your playlist. 
Copy them!

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/API2.png)

The third step is click this website, and login with Spotify.
```
https://www.spotlistr.com/search/textbox
```
You can paste the songs' name list what you got from the second step here, after login. 
Like this:

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/SPO1.png)

Click the "Search" button, and wait for the result. 

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/SP2.png)

The last step is scrolling to the botteom of this screen, and give your new playlist an amazing name! After that, click "create", and this new amazing playlist will import to your Spotify automatically!
Enjoy it!!!

![image](https://github.com/DonaldOffical/To-Spotify/blob/main/images/SPO3.png)

AND IF YOU ARE INTERESTED IN THE CODE VERSION, THERE IS SOME CODE BASED ON PYTHON 3 FROM bjason. (RESPECT TO bjason AGAIN)
```
import json
import sys
import urllib.request

# using API provided by dongyonghui(https://github.com/mrdong916)
# instruction page: www.dongyonghui.com/default/20180128-网易云、酷狗、QQ音乐歌单接口API.html

welcome = "===== Get tracks of your 163 playlist ====="
enterId = "Enter the playlist id (Enter ? to get help):"
help = "To get the id of the playlist, go to the page\
of it and look at the address bar.\
 \nPlaylist id is the numbers after \
 'http://music.163.com/#/playlist?id='"
errRetrive = "No data retrived. \nPlease check the playlist id again."

while 1:
	print(welcome)
	playlistId = input(enterId)

	#change the playlistId variable 
	if playlistId == "?":
		print(help)
		continue
		
	# transCode 020111 assigns to retrieve playlist from 163 music
	postContent = {"TransCode":"020111","OpenId":"123456789","Body":{"SongListId":playlistId}}
	encodedContent = json.dumps(postContent).encode('utf-8')
	
	reqUrl = "https://api.hibai.cn/api/index/index"
	
	req = urllib.request.Request(reqUrl)
	req.add_header('Content-Type', 'application/json; charset=utf-8')
	req.add_header('Accept', 'application/json')
	
	response = urllib.request.urlopen(req, encodedContent).read().decode('utf-8')
	data = json.loads(response)
	
	output = ""

	if data["ErrCode"] != "OK":
		print(data["ErrCode"])
		print(errRetrive)
		print(help)
		continue
		
	body = data["Body"]
	playlistName = body["name"]
	tracks = body["songs"]
	
	for track in tracks:
		trackName = track["title"]
		artist = track["author"]
		output += trackName + " - " + artist + "\n" 
	
	with open(playlistName + ".txt", "w", encoding="utf-8") as file:
		file.write(output)

	print("===== Success =====\nCheck the directory of this file and find the .txt file!")
	print
  ```
  
  
