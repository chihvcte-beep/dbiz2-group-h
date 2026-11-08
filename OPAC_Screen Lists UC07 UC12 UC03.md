# Screen List -- UC-07, UC-12 and UC-03

This document consolidates the screen lists for three use cases in the
OPAC project. The screen IDs follow the `S-<feature>-<nn>` convention.
The project extends the existing OPAC rather than creating a completely
new system.

------------------------------------------------------------------------

# UC-07 -- Update and View Personal Reading History and Preferences

**Actor:** Reader\
**Feature:** F-03\
**Login required:** Yes

## Screen List

  ---------------------------------------------------------------------------------------------------------------------------------
  Screen ID  Screen name   Actor    Feature   Shown when    Entry points Use cases / Priority   Screen spec
                                              (purpose)                  FRs served             
  ---------- ------------- -------- --------- ------------- ------------ ----------- ---------- -----------------------------------
  S-F03-01   Reading       Reader   F-03      A signed-in   Entry point  UC-07 ·     Should     `screens/screen-spec-S-F03-01.md`
             History                          reader wants  not          FR-03-01,              
                                              to view their specified in FR-03-04               
                                              personal      the project                         
                                              reading       documents.                          
                                              history,                                          
                                              including the                                     
                                              books                                             
                                              recorded in                                       
                                              their history                                     
                                              and their                                         
                                              reading                                           
                                              status. The                                       
                                              reader can                                        
                                              also update a                                     
                                              book's                                            
                                              reading                                           
                                              status                                            
                                              (Reading or                                       
                                              Finished) and                                     
                                              manually                                          
                                              enter reading                                     
                                              progress.                                         

  S-F03-02   Reading       Reader   F-03      A signed-in   Entry point  UC-07 ·     Could      `screens/screen-spec-S-F03-02.md`
             Preferences                      reader wants  not          FR-03-05               
                                              to set and    specified in                        
                                              save personal the project                         
                                              reading       documents.                          
                                              preferences                                       
                                              in their                                          
                                              profile.                                          
  ---------------------------------------------------------------------------------------------------------------------------------

## Modals and overlays

No modals or overlays are identified in the project documents for UC-07.

## What is deliberately not a screen

  -----------------------------------------------------------------------
  Candidate                           Why it is not a screen
  ----------------------------------- -----------------------------------
  Automatically add a history entry   An automatic system event
  when an online book is opened or    (FR-03-02); it does not require a
  downloaded                          separate user interface.

  Add history entries from borrowed   Background processing based on
  physical books                      synchronised loan records
                                      (FR-03-03); it does not require a
                                      separate user interface.

  Update reading status and progress  An action performed on the Reading
                                      History screen (FR-03-04), not a
                                      separate screen.

  Sign in                             A shared platform screen
                                      (`S-F00-01`), not specific to
                                      UC-07.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# UC-12 -- Save Physical Books to a Personal List and Remove Them

**Actor:** Reader\
**Feature:** F-03\
**Login required:** Yes

## Screen List

  ---------------------------------------------------------------------------------------------------------------------------
  Screen ID  Screen   Actor    Feature   Shown when   Entry points Use cases / Priority   Screen spec
             name                        (purpose)                 FRs served             
  ---------- -------- -------- --------- ------------ ------------ ----------- ---------- -----------------------------------
  S-F03-03   Book     Reader   F-03      A signed-in  Existing     UC-12 ·     Should     `screens/screen-spec-S-F03-03.md`
             Detail                      reader views OPAC book    FR-03-06               
                                         the details  search                              
                                         of a         results →                           
                                         physical     Book Detail                         
                                         book and                                         
                                         selects the                                      
                                         Save action                                      
                                         to add it to                                     
                                         their                                            
                                         personal                                         
                                         saved books                                      
                                         list. The                                        
                                         Save action                                      
                                         is available                                     
                                         for physical                                     
                                         books.                                           

  S-F03-04   Saved    Reader   F-03      A signed-in  Entry point  UC-12 ·     Should\*   `screens/screen-spec-S-F03-04.md`
             Books                       reader views not          FR-03-07,              
             List                        their saved  specified in FR-03-08               
                                         physical     the project                         
                                         books        documents.                          
                                         together                                         
                                         with their                                       
                                         shelf                                            
                                         locations.                                       
                                         The reader                                       
                                         can also                                         
                                         select                                           
                                         Remove to                                        
                                         delete a                                         
                                         book from                                        
                                         the list.                                        
  ---------------------------------------------------------------------------------------------------------------------------

**Priority note:** The Saved Books List is marked Should because its
main requirement (FR-03-07) is Should. The Remove action (FR-03-08) is
Could.

## Modals and overlays

No modals or overlays are identified in the project documents for UC-12.

## What is deliberately not a screen

  -----------------------------------------------------------------------
  Candidate                           Why it is not a screen
  ----------------------------------- -----------------------------------
  Save a physical book                An action performed on the existing
                                      Book Detail screen (FR-03-06), not
                                      a separate screen.

  Remove a saved book                 An action performed on the Saved
                                      Books List screen (FR-03-08), not a
                                      separate screen.

  Save/removal confirmation           A success state; the project
                                      documents do not specify a
                                      dedicated page or dialog.

  Sign in                             A shared platform screen
                                      (`S-F00-01`), not specific to
                                      UC-12.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# UC-03 -- Filter Books by Access Format (Online, Physical or Both)

**Actor:** Reader\
**Feature:** F-03\
**Login required:** No

## Screen List

  -------------------------------------------------------------------------------------------------------------------------
  Screen ID  Screen     Actor    Feature   Shown when  Entry      Use cases  Priority   Screen spec
             name                          (purpose)   points     / FRs                 
                                                                  served                
  ---------- ---------- -------- --------- ----------- ---------- ---------- ---------- -----------------------------------
  S-F03-05   Search     Reader   F-03      A reader    Existing   UC-03 ·    Should     `screens/screen-spec-S-F03-05.md`
             Results --                    wants to    OPAC       FR-03-12              
             Advanced                      narrow down search →                         
             Filter                        book search Search                           
             Panel                         results by  Results →                        
                                           access      Advanced                         
                                           format. The Filter                           
                                           reader can  Panel                            
                                           select an                                    
                                           access                                       
                                           format, and                                  
                                           the system                                   
                                           displays                                     
                                           only books                                   
                                           available                                    
                                           in the                                       
                                           selected                                     
                                           format.                                      

  -------------------------------------------------------------------------------------------------------------------------

## Modals and overlays

No modals or overlays are identified in the project documents for UC-03.
The access-format filter is part of the Advanced Filter Panel, not a
separate modal or page.

## What is deliberately not a screen

  -----------------------------------------------------------------------
  Candidate                           Why it is not a screen
  ----------------------------------- -----------------------------------
  Apply access format filter          An action performed within the
                                      Advanced Filter Panel (FR-03-12).

  Display filtered search results     A result state of the existing
                                      Search Results screen after the
                                      selected filter is applied.

  Log anonymous online-book reads     A system event that records the
                                      book ID and read time without
                                      reader identity (FR-03-13); it does
                                      not require a separate user
                                      interface.

  View access formats of a book       Excluded from the project scope
                                      (FR-03-14, Won't). The existing
                                      OPAC already displays access-format
                                      information.

  Download PDF of an online book      Excluded from the project scope
                                      (FR-03-15, Won't). The existing
                                      OPAC already supports PDF
                                      downloads.
  -----------------------------------------------------------------------

**Scope note:** FR-03-12 is the in-scope access-format filtering
requirement. FR-03-14 and FR-03-15 are marked Won't and are therefore
not included as new screens or new functionality in this project.

------------------------------------------------------------------------

## Screen ID Summary

  Screen ID   Screen name                               Use case
  ----------- ----------------------------------------- ----------
  S-F03-01    Reading History                           UC-07
  S-F03-02    Reading Preferences                       UC-07
  S-F03-03    Book Detail                               UC-12
  S-F03-04    Saved Books List                          UC-12
  S-F03-05    Search Results -- Advanced Filter Panel   UC-03
