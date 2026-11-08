flowchart TD  
  classDef screen fill:\#e1f5fe,stroke:\#0288d1,stroke-width:2px,color:\#01579b;  
  classDef decision fill:\#fff3e0,stroke:\#f57c00,stroke-width:2px,color:\#e65100;  
  classDef modal fill:\#f3e5f5,stroke:\#7b1fa2,stroke-width:1.5px,stroke-dasharray:4 4,color:\#4a148c;  
  classDef goal fill:\#e8f5e9,stroke:\#2e7d32,stroke-width:2px,color:\#1b5e20;  
  classDef action fill:\#ffffff,stroke:\#757575,stroke-width:1px,color:\#212121;

  %% Entry points and authentication  
  Start(\["Reader enters OPAC Platform"\]):::goal \--\> EntryChoice{"Choose Discovery Path"}:::decision

  EntryChoice \--\>\|"Click 'Recommended for You'"\| CheckAuthRec{"Signed in?"}:::decision  
  CheckAuthRec \--\>\|"Yes"\| S\_Rec  
  CheckAuthRec \--\>\|"No"\| M\_AuthRec\["Modal: Prompt Sign-In (M-F03-07-01)"\]:::modal  
  M\_AuthRec \--\>\|"Proceed to Sign In; store returnTo \= Recommendations"\| S\_SignIn\["S-F00-01: Sign In Screen (UC-11)"\]:::screen  
  M\_AuthRec \--\>\|"Cancel"\| EntryChoice

  EntryChoice \--\>\|"Click AI Chat Widget"\| CheckAuthChat{"Signed in?"}:::decision  
  CheckAuthChat \--\>\|"Yes"\| S\_Chat  
  CheckAuthChat \--\>\|"No"\| M\_AuthChat\["Modal: Prompt Sign-In (M-F03-06-01)"\]:::modal  
  M\_AuthChat \--\>\|"Proceed to Sign In; store returnTo \= Chatbot"\| S\_SignIn  
  M\_AuthChat \--\>\|"Cancel"\| EntryChoice

  S\_SignIn \--\>\|"Success OTP"\| ReturnDestination{"Stored returnTo?"}:::decision  
  ReturnDestination \--\>\|"Recommendations"\| S\_Rec  
  ReturnDestination \--\>\|"Chatbot"\| S\_Chat  
  S\_SignIn \--\>\|"Invalid OTP: show error and retry"\| S\_SignIn  
  S\_SignIn \--\>\|"Expired OTP: request new code"\| S\_SignIn  
  S\_SignIn \--\>\|"Cancel sign-in"\| EntryChoice

  %% UC-09: Recommendations  
  subgraph UC09\_Flow \["UC-09: Automatic Recommendations Flow"\]  
    S\_Rec\["S-F03-07: Book Recommendations Screen"\]:::screen  
    S\_Rec \--\> RecCondition{"Reader profile state?"}:::decision  
    RecCondition \--\>\|"Cold-start: no history or preferences"\| S\_Rec\_Cold\["Display Popular Books"\]:::action  
    RecCondition \--\>\|"Has history / preferences"\| S\_Rec\_Personal\["Display Personalised Book Grid"\]:::action  
    S\_Rec\_Cold \--\>\|"Click 'Tune Preferences'"\| S\_Pref\["S-F03-02: Reading Preferences (UC-07)"\]:::screen  
    S\_Pref \--\>\|"Save preferences"\| S\_Rec\_Personal  
    S\_Rec\_Personal \--\>\|"Click 'Tune Preferences'"\| S\_Pref  
  end

  S\_Rec\_Personal \--\>\|"Ask specific topic about suggestion"\| S\_Chat

  %% UC-08: AI chatbot search  
  subgraph UC08\_Flow \["UC-08: AI Chatbot Search Flow"\]  
    S\_Chat\["S-F03-06: AI Chatbot Book Search Screen"\]:::screen  
    S\_Chat \--\> ChatAction\["Type natural language inquiry"\]:::action  
    ChatAction \--\> ChatResult{"AI Service response?"}:::decision  
    ChatResult \--\>\|"Matching books found"\| S\_Chat\_Cards\["Display Book Result Cards in chat"\]:::action  
    ChatResult \--\>\|"No exact match"\| S\_Chat\_NoMatch\["Display No-match advice & topic chips"\]:::action  
    ChatResult \--\>\|"Timeout / Error"\| S\_Chat\_Err\["Display Error warning & Link to Filter"\]:::action  
    S\_Chat\_NoMatch \--\>\|"Select alternative chip or rephrase"\| ChatAction  
    S\_Chat\_Cards \--\>\|"Ask another question"\| ChatAction  
    S\_Chat\_Err \--\>\|"Retry inquiry"\| ChatAction  
  end

  %% UC-03: Advanced filtering  
  subgraph UC03\_Flow \["UC-03: Advanced Format Filter"\]  
    S\_Filter\["S-F03-05: Advanced Format Filter"\]:::screen  
    S\_Filter \--\>\|"Apply filters"\| FilterResult{"Matching books found?"}:::decision  
    FilterResult \--\>\|"Yes"\| FilterCards\["Display Filtered Book Results"\]:::action  
    FilterResult \--\>\|"No: show no-results message and adjust filters"\| S\_Filter  
    FilterCards \--\>\|"Change filters"\| S\_Filter  
  end

  S\_Chat\_Err \--\>\|"Click fallback filter"\| S\_Filter

  %% Post-discovery screens and actions  
  subgraph Post\_Discovery \["Post-Discovery Actions (UC-01 & UC-12)"\]  
    S\_Detail\["S-F03-03: Book Detail Screen"\]:::screen  
    S\_Map\["S-F01-01: Shelf Location & Map"\]:::screen  
    S\_SaveSuccess\["Save book to profile"\]:::action  
    S\_SavedList\["S-F03-04: Saved Books List Screen"\]:::screen

    S\_Detail \--\>\|"Click 'Find Shelf Location'"\| S\_Map  
    S\_Detail \--\>\|"Click 'Save to List'"\| S\_SaveSuccess  
    S\_SaveSuccess \--\>\|"Book saved successfully"\| S\_SavedList  
    S\_SavedList \--\>\|"Click saved book"\| S\_Detail  
  end

  %% Connect discovery results to book actions  
  S\_Rec\_Cold \--\>\|"Click Book Card"\| S\_Detail  
  FilterCards \--\>\|"Click Book Card"\| S\_Detail  
  S\_Chat\_Cards \--\>\|"Click Book Card"\| S\_Detail  
  S\_Rec\_Personal \--\>\|"Click Book Card"\| S\_Detail  
  S\_Chat\_Cards \--\>\|"Click 'Shelf Location' link"\| S\_Map  
  S\_Rec\_Personal \--\>\|"Click 'Shelf Location' link"\| S\_Map  
  S\_Chat\_Cards \--\>\|"Click 'Save Book' icon"\| S\_SaveSuccess  
  S\_Rec\_Personal \--\>\|"Click 'Save Book' icon"\| S\_SaveSuccess

  %% Goals within the platform scope  
  S\_Map \--\> Goal1(\["Goal Met: View shelf location for the selected book"\]):::goal  
  S\_SavedList \--\> Goal2(\["Goal Met: Book saved for library visit"\]):::goal  
