This information is also available on my blog, and link are as below.  
[Basic Voting Machine GUI using MATLAB](https://embeddedlaboratory.blogspot.com/2017/07/voting-machine-gui-demo-using-matlab.html)  
[Advanced Voting Machine GUI using MATLAB](https://embeddedlaboratory.blogspot.com/2018/01/advance-voting-machine-gui-demo-using.html)  

_Note: There are two versions of Voting one is basic and the another is advanced with some more features, basic version is present at_ `Tag v1.0` _and advance is present at_ `Tag v2.0` _so please choose accordingly and don't forget to read the description below for advanced one also._  

# Voting Machine GUI Demo Using MATLAB
Electronic voting machines (EVMs) are used to conduct elections in India and several other countries. These machines provide straightforward and effortless features to voters to cast their votes in favor of their party members.  
When a voter presses a button adjacent to the name of the candidate, a beeping sound is made by the EVM, confirming successful casting of vote, and the vote count of that particular candidate increases by one.  
In this project, a demo software program using MATLAB based graphical user interface (GUI) to demonstrate the working of an EVM is presented. A screenshot of the EVM using MATLAB GUI is shown below.  

![Voting Machine GUI in MATLAB](https://3.bp.blogspot.com/-5tso63TjMTY/WXTIvNld7eI/AAAAAAAAAjs/Jh6IWG0xpCwRtutwslENEeO3xrSJAmf3QCLcBGAs/s1600/VotingMachine.PNG)  

So in this project, 5 candidates or party's are considered in election. And then for each party candidate there is a button available adjacent to it's name, which when pressed increases the vote count of that particular candidate or party by one.  
Once the complete voting is finished, Results button can be used to display the results, which includes which total votes received by a particular party along with their voting percentage.  

[Watch this video to view the working demo of this project](https://www.youtube.com/watch?v%3DwmxsZhtGPGo)

## Construction
GUIDE is used to develop the GUI for this demo project, with components like `Static Text` to display Party Name, Votes, Votes Percentage, and `Push Button` components are used as Vote, Result and Reset Buttons.  
The logic is this demo project is very simple, for each party we have created a global variable, which is declared and initialized as shown below.  

```matlab
% --- Executes just before VotingGUI is made visible.
function VotingGUI_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% varargin   command line arguments to VotingGUI (see VARARGIN)

% Choose default command line output for VotingGUI
handles.output = hObject;

% Update handles structure
guidata(hObject, handles);

% UIWAIT makes VotingGUI wait for user response (see UIRESUME)
% uiwait(handles.figure1);
global party1;
global party2;
global party3;
global party4;
global party5;

party1 = 0;
party2 = 0;
party3 = 0;
party4 = 0;
party5 = 0;
```

As you can see in the above piece of code, 5 global variables are defined for each party.  
Now we have to create a callback and update these variables whenever the voting button is pressed, which is shown below.  
```matlab
% --- Executes on button press in pushbtn_party1.
function pushbtn_party1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbtn_party1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global party1;
party1 = party1+1;
```

The same thing will be done for other party members, and after this we can determine the election results by pressing the result button, the calculation for determining the Voting Percentage is very simple.  
```
Vote Percentage(%) Party 1 = (Total Votes Received by Party 1 * 100)/ Total Votes
```

So we used the same formula in MATLAB, and is as shown below.  
```matlab
% --- Executes on button press in pushbtn_results.
function pushbtn_results_Callback(hObject, eventdata, handles)
% hObject    handle to pushbtn_results (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global party1;
global party2;
global party3;
global party4;
global party5;

total_votes = party1+party2+party3+party4+party5;

set(handles.text_party1_votes, 'String', party1);
set(handles.text_party2_votes, 'String', party2);
set(handles.text_party3_votes, 'String', party3);
set(handles.text_party4_votes, 'String', party4);
set(handles.text_party5_votes, 'String', party5);

set(handles.text_party1_votes_per, 'String', party1*100/total_votes);
set(handles.text_party2_votes_per, 'String', party2*100/total_votes);
set(handles.text_party3_votes_per, 'String', party3*100/total_votes);
set(handles.text_party4_votes_per, 'String', party4*100/total_votes);
set(handles.text_party5_votes_per, 'String', party5*100/total_votes);

set(handles.text_total_votes,  'String', total_votes);
```
So that's all, by doing this you can develop your small Voting Machine GUI in MATLAB.  


**Note:**
This post presents a simulation of the working of the Voting Machines, you can make Voting Machine  with hardware like Arduino board, as a replacement of `Push Button` you need switches and to display results you can use Seven Segment or LCD or Graphical LCD or you can also use PC to display the results.  

# Advanced Voting Machine GUI Demo Using MATLAB
In the upper post we have shared a project named `Voting Machine based on MATLAB GUI`, this project was very basic in nature, and in this section we are going to add few more scenarios to make this system more useful and practical.  
![Advanced Voting GUI in MATLAB](https://3.bp.blogspot.com/-31x3CZ9Gchg/Wln88kYvwzI/AAAAAAAAAmA/oKlp7Z-nBAci1sNcVxyM2Rch-3JN0CaCgCLcBGAs/s1600/VotingGUI.PNG)  

Some of the additional feature of this project are as follow:
* Voters who's names and Id's are present in Database can only vote.
* Duplicate Voting is not allowed.
* Voting Percentage is also calculated.

So with the above mentioned features one can create a more robust and professional system.  
To create database, Microsoft Excel is used and names of voters and there voting id's are written in two different columns. For this project a sample database of 10 voters is created and is shown in the image given below.  

![Enter Voting ID](https://2.bp.blogspot.com/-R_LRho1Z3yA/WloBTmRIFWI/AAAAAAAAAm0/ADc2kZ0X-z0EcoqC1Ln4gH6gvRC9AQ10gCEwYBhgL/s1600/Voter%2BID.PNG)  

There are two cases now, one if voting id exist and in another case, it doesn't exist. System will display following screens in these two cases.  
* Case 1: If Voter Id exist, the system will greet voter with message "Thank You" as shown below.
![Thank You for Voting](https://4.bp.blogspot.com/-pXAd6zEpkn0/WloBTDooySI/AAAAAAAAAmw/Gr2e8qtlW5kBmQ_hNp34Tx5zhnvNnPtUQCEwYBhgL/s1600/Vote%2BSuccess.PNG)  

* Case 2: If Voter Id doesn't exist, the system will generate an error, as shown below.
![User Not Found](https://3.bp.blogspot.com/-E0h7KVWypAA/WloDT1_1STI/AAAAAAAAAnA/Nzw9tQERduI1oJftPTiX6x8jM6Cy3a9BgCLcBGAs/s1600/Voter%2Bnot%2BFound.PNG)  

Now coming to the another case, when voter is trying to enter vote twice, so in this case system will generate a message that you can't vote multiple times as shown below.  
![Multiple Votes Not Allowed](https://1.bp.blogspot.com/-wmLQ6_3CjEw/WloBTGQfYOI/AAAAAAAAAms/JQPuPOPwZ7QCWe65VqBmJjKqGHAZ7RTwwCEwYBhgL/s1600/Vote%2BDuplicate.PNG)  

And then finally on pressing the result button, results are shown on the screen as follow.  
![Results](https://1.bp.blogspot.com/-4Ye7Wl4cr9E/WloBTNjuq6I/AAAAAAAAAm4/ftFMTOm_bFYJXXmmZU0-u-wehom1H4WKACEwYBhgL/s1600/Results.PNG)  

## Source Code
There are basically two main parts of the project, one is loading and storing the data and another is using this data to increase the vote count or display messages or error to the voters.  
Coming to the first part, i.e loading the Excel file data into MATLAB, this is done using the following piece of code.  
```matlab
global voters_name;
global voters_id;
global voting_status;

% Open Voter ID List File
filename = 'VotingList.xlsx';
[~, ~, raw] = xlsread(filename);
voters_name = raw(2:end, 2);
voters_id = raw(2:end, 3);
% Create voting status variable to keep track of person's who already voted
voting_status = zeros(numel(voters_name), 1);
```

As can we seen in above code, three new global variables are declared, voters_name will contain the names of all voters, voters_id will contain the voter ids and voting_status variable is initialized to zero, this variable will keep track if a voter has given his vote or not.  

Now coming to second and most important part, where decision is made if a voter is a legal voter or not. 
```matlab
global party1;
global voters_name
global voters_id
global voting_status

prompt = {'Enter your Voter ID ?'};
dlg_title = 'Input';
num_lines = 1;
defaultans = {'1234567890'};
answer = inputdlg(prompt,dlg_title,num_lines,defaultans);
index = find([voters_id{:}] == str2double(answer));
if index
  %disp (voters_name(index));
  name = string(voters_name(index));
  if voting_status(index) == 0
    party1 = party1+1;
    % Voting Done
    voting_status(index) = 1;
    msgbox(sprintf('Thank you "%s" for voting',name),'Vote Success')
  else
    msgbox(sprintf('"%s" you cant give vote multiple times', name),'Duplicate')
  end
else
  errordlg('User Not Found','Database Error');
end
```
As can be seen in the above code, Voter ID is prompted on screen and then this voter id is used to search, in database, if match is found then, system will check if this voter has given vote earlier or not, if not given, voter status will be updated so that voter can't vote multiple times.  

[YouTube Video](https://youtu.be/TepDXW0ShXs)  

**Future Possibilities**
The above system has limitation, that if someone else remembers your voting ID, then that voter can give your vote, to overcome this situation and make system more interesting, Bio-metric system or finger print scanner can be added to this project, if we get time, we will definitely post this project also.  