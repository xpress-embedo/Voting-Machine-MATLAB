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