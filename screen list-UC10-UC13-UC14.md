# Screen List: Library Core System (Group H)

**Screen ID pattern:** `S-<feature>-<nn>`. Shared screens use
`S-F00-<nn>`.

  -----------------------------------------------------------------------------------------------------------------------------
  Screen ID  Screen name  Actor     Feature   Shown when  Entry      Use cases / Priority   Screen spec
                                              (purpose)   points     FRs served             
  ---------- ------------ --------- --------- ----------- ---------- ----------- ---------- -----------------------------------
  S-F04-01   Staff        On-site   F-04      Staff needs Staff page UC-10,      Must       `screens/screen-spec-S-F04-01.md`
             sign-in &    Staff               to access   entry;     UC-13 ·                
             staff page                       the staff   direct     FR-04-07,              
             menu                             page to     access     FR-04-08               
                                              print QR    while                             
                                              labels or   signed out                        
                                              manage                                        
                                              reported                                      
                                              reviews                                       

  S-F02-01   QR label     On-site   F-02      Staff       Staff page UC-10 ·     Must       `screens/screen-spec-S-F02-01.md`
             printing &   Staff               selects     menu in    FR-02-08               
             preview                          physical    S-F04-01                          
                                              books and                                     
                                              previews a                                    
                                              printable                                     
                                              sheet of QR                                   
                                              code labels                                   

  S-F02-02   Book reviews Reader    F-02      Reader      Book       UC-05,      Could      `screens/screen-spec-S-F02-02.md`
                                              views       details;   UC-14 ·                
                                              reviews of  QR code    FR-02-09               
                                              a book and  scan;                             
                                              chooses to  reviews                           
                                              report a    section                           
                                              review that                                   
                                              appears to                                    
                                              violate the                                   
                                              rules                                         

  S-F02-03   Reported     On-site   F-02      Staff views Staff page UC-13,      Could      `screens/screen-spec-S-F02-03.md`
             reviews      Staff               reported    menu in    UC-14 ·                
             management                       reviews,    S-F04-01   FR-02-10,              
                                              inspects a             FR-04-08               
                                              selected                                      
                                              review and                                    
                                              chooses to                                    
                                              remove it                                     
                                              from public                                   
                                              display                                       
  -----------------------------------------------------------------------------------------------------------------------------

## Modals and overlays

  -----------------------------------------------------------------------
  Modal                   Opened from screen      Purpose
  ----------------------- ----------------------- -----------------------
  Confirm review removal? S-F02-03                Allow On-site Staff to
                                                  confirm removal of a
                                                  selected reported
                                                  review from public
                                                  display

  Report submitted        S-F02-02                Display confirmation
                                                  after the report has
                                                  been successfully saved
                                                  against the selected
                                                  review
  -----------------------------------------------------------------------

## What is deliberately not a screen

  -----------------------------------------------------------------------
  Candidate                           Why it is not a screen
  ----------------------------------- -----------------------------------
  Automatic QR code generation        Background system process triggered
  (UC-10)                             when a new physical book appears in
                                      the synced catalogue; no user
                                      interaction is required (FR-02-07).
                                      Online-only books do not receive QR
                                      codes.

  Staff access denied                 Error state of S-F04-01 when staff
                                      credentials or the required session
                                      are invalid (FR-04-08).

  QR code generation success          Background processing result; the
                                      QR code is generated automatically
                                      and linked to the physical book
                                      (FR-02-07).

  Report review action                An action within S-F02-02, not a
                                      separate screen (FR-02-09).

  Review removal success              Success state of S-F02-03 after
                                      staff confirms removal (FR-02-10).

  Reader sign-in (UC-11)              Existing account sign-in use case;
                                      UC-14 reuses this flow rather than
                                      introducing a new sign-in screen.
  -----------------------------------------------------------------------
