
+-=== SQ8Light VST (v0.91 beta) ===================================-+

   Programming & design by Siegfried Kullmann

   Factory sounds in bank C by Ole Jeppesen & Siegfried Kullmann
   Bank D contains sounds by Ensoniq taken from the SQ80.

   (C)opyright 2006-2008
   Mail: sigi.kullmann@googlemail.com

   Thanks to
   Rainer Buchty
   for SQ80 resources & disassembled OS code
   Homepage: http://www.buchty.net

   Cubase and VST are trademarks of 
   Steinberg Media Technologies GmbH.

   Ensoniq, ESQ1 and SQ80 are trademarks of
   ENSONIQ Corp.



+-=== Notes on the factory sounds =================================-+


   Most factory sounds use the modulation wheel, but some also use
   the breath controller (midi controller #2).
   Please be aware that that some sounds use special SQ8L features
   and thus are not fully compatible with the real synths SQ80/ESQ1.

   Unfortunately, there wasn't enough time to create sounds which take
   advantage of the features new in this version (0.91b).

+-=== Contents ====================================================-+


   A. Installation
   B. What is SQ8L?
   C. Version history
   D. Synthesis
   E. The user interface
   F. Known problems
   G. Things to come...



+-=== A. Installation =============================================-+


   --- Installation -------------------------------------------------

   Extract all files including sub folders from the archive to the
   folder containing your VST plugins.

   
   --- Installing over versions below 0.90b -------------------------

   Like above, but the sub folder "data\" will no longer be used
   and can be deleted (remember to backup the file
   "data\SQ8L_backup.dat" if you need it!).
   The folder "user\" is no longer used to store the factory
   library as it is included in the plugin.


   --- Installing over versions below 0.83a -------------------------

   You can just copy the new version over the old one.
   The older versions created an entry in the Windows registry
   which will be no longer needed. Just open "regedit", find
   and delete the entry "HKEY_LOCAL_MACHINE\SOFTWARE\SQ8L".



+-=== B. What is the SQ8L? ========================================-+


   The SQ8L is a software model (VST) of Ensoniq's classic 1980s
   synth SQ80. The SQ80 features 3 digital wavetable oscillators
   for each of its 8 voices which are fed through analog 4-pole
   lowpass filters (-24dB gain) with resonance. Sound parameters can
   be modulated by 4 envelopes, 3 LFOs and several MIDI sources.
   The SQ80 also has a predecessor, the ESQ1, which can do most of
   the same stuff.
   Although the technology may seem obsolete, these synths can
   produce a wide variety of interesting and extremely usable sounds.
   Thanks to the lo-fi oscillators and the analog components it can
   sound very digital and dirty, but also very analog and warm.
   Which is a good thing because modern synths often tend to sound
   rather clean. Now you can experience this great classic synth
   with the SQ8L!

   The SQ8L ("L" stands for "Light") is the free demo version of the
   forthcoming SQ8X ("X" for "eXtended"). Besides any bugs that will
   (hopefully) be removed in the full version (see "Known problems")
   and planned features that won't find their way into the light
   version (see "Things to come..."), there are only a few
   limitations. Those are:

      - Polyphony limited to 8 voices.
      - Program change messages ignored.
      - When used with a sequencer, the only sound the host can save
        within the song file is the one in the edit buffer.
      - No Split/Layer to combine several sounds.
      - No internal sequencer (and there will never be one).
      - No automation (only MIDI input).



+-=== C. Version history ==========================================-+


  --- 0.91 beta --------------------------------------------------

    - Parameter changes now immediately affect playing voices
      (except envelope parameters).
    - Fixed bug in DCA4 modulation causing voices to be never
      terminated.
    - Fixed problem with high CPU load after playing one-shot
      waveforms.
    - Voice restart should work correctly now.
    - LOOP voice stealing mode removed. The former HQ mode is now
      called SOFT.

    - New LFO implementation with much more accurate frequency and
      delay and the following new features (see paragraph D.2.):
        - Humanization (randomize LFO frequency).
            ON = emulate SQ80/ESQ1 (no humanization for frequencies<7
                 or while fading)
            1x = humanize always
            2x, 4x, 8x, 16x = humanize more
        - All waveforms of OSC1-3 can be used for LFOs (except the
           drum kits)
        - Frequency modulation (FREQMOD).
        - Adjustable phase offset (PHS) (in addition to trigger phase).
        - Twin mode (PHS parameter, indicated by "T" in the value):
          Two phase-shifted waves are subtracted from each other.
        - 4 Playback modes (PLAY):
            FWD = forward
            REV = reversed (=backwards)
            1XF = one-shot forward
            1XR = one-shot reversed
        - Smoothing (SMTH, applied before amplitude modulation).
        - Different modes for amplitude/frequency modulators (AM, FM):
            UNI = unipolar (source is clipped below zero, used to
                  correctly emulate the AM of SQ80/ESQ1 LFOs)
            BIP = bipolar (was incorrectly used for AM until this version)
            PHS = modulate LFO phase offset instead
            SMT = modulate LFO smoothing instead
        - Modes for LFO delay:
            EMU = emulate SQ80/ESQ1
            SMTH = smoother fading
        - Frequency range extended from 0..63 to 0..127

    - New envelope features (see paragraph D.3.):
        - Start level (L0) instead of fixed to zero.
        - CYC parameter for each envelope (=play full cycle without
          sustain).
        - Smoothing filter (SMTH).
        - Parameter MODE-T1V switches between:
            T1 = Velocity modulates attack time (T1) by amount in T1V
            SMT = Velocity modulates smoothness (SMTH) by amount in T1V
        - Different output shapers (SHAPE):
            OFF = no shaping
            EXP..EXP4 = exponential shaping
            TAN..TAN3 = hyperbolic tangent shaping

    - New emulation features (see also paragraph D.1.):
        - Smoothing of DCA1-3 volumes:
            EMU = emulate SQ80/ESQ1
            FAST = less accurate but without latency
        - Smoothing of DCA4 volume:
            EMU = emulate SQ80/ESQ1 (soft attack)
            HARD = hard attack
        - MUFFLE:
            OFF = crisp sound
            ON = attenuate high frequencies to sound more like
                 the SQ80/ESQ1
        - DC offset blocking filter (DC-BLOCK):
            SMART = use filter when needed (when SYNC=ON)
            ON = always on
            OFF = always off


    - Changes in sound banks:
      - Banks A, B = user banks
      - Bank C = SQ8L factory bank
      - Bank D = original SQ80 factory bank

    - GUI changes:
      - Bigger GUI with buttons to select parameter pages
        (see paragraph E.3.).
      - Most display pages can now be scrolled/toggled to show
        additional parameters (see paragraph E.2.)
      - Fixed bug with window scaling causing wrong placement of
        GUI controls (has not been tested).
      - Fixed problems with "jumping mouse" (I hope so).
      - The knobs and buttons should no longer steal the keyboard
        focus (has not been tested).
      - Several emulation parameters can be overriden by settings
        in the options menu.
      - Added modulation source usage window (temporary, see paragraph
        E.4.).

      
  --- 0.90 beta --------------------------------------------------

    - New voice management and voice stealing mechanism.
    - Fixed problems with monophonic glide.
    - Restart-Voice now correctly implemented.
    - Fixed bug causing clicks when using GLIDE together with SYNC.
    - Oscillators now working almost perfectly:
        - Fixed (de)tuning problems.
        - Waveforms like NOISE2 now played correctly.

    - Fixed low volume. The SQ8L is really loud now!
    - Amplitude is decreased with increasing saturation amount.
    - New shapers for DCA1-4 resulting in smoother and more authentic
      modulation.
    - Panning issues:
       - Changed modulation range from -63..+63 to -127..+127.
         The range -63..+63 matches with the SQ80/ESQ1.
       - Fixed SQ80/ESQ1 SysEx import/export.

    - The following midi controllers are now recognized (see also
      below under "Synthesis"):
         7 (07 hex) : Master volume
        10 (0A hex) : Panning
        11 (0B hex) : Expression
        64 (40 hex) : Hold/Sustain pedal
        74 (4A hex) : Brightness
    - Key pressure (polyphonic aftertouch) works now.
    - Filter resonance slightly increased.
    - Range of filter modulation amount changed from -63..+63 to
      -127..+127. The range -63..+63 matches with the SQ80/ESQ1.

    - Pitch bend now available as modulation source.
    - Default pitch bend range is now 2 semitones (also changed
      in most factory sounds).

    - GUI changes:
      - New design, keyboard removed.
      - New sound compare function in the WRITE dialog.
      - Parameters on the LCD and knobs can now both be used in
        the same way (double clicking, mouse dragging).
      - The sound selection popup menu can now also be opened by
        right-clicking the sound program name.
      - Saturation (SAT) parameter moved from emulation page to DCA4.
      - Faster popup menus (noticable on slow computers).
      
    - New file format for sound libraries (!).
    - Soundbanks:
       - Bank A (write proteced) contains the factory sounds
       - Bank b is the user bank 
    - SQ8L settings and sound library now global (correctly shared
      among SQ8L instances).
    - Waverom integerated into DLL (folder "\data" no longer used).

  --- ...zZZZzz... ------------------------------------------------

  --- 0.84 alpha --------------------------------------------------

    ! Note on this release:
        This version sounds different from earlier versions, so
        when using this in an older mix, you may have to do some
        adjustments. Sorry for any inconveniences!

    - New filter which is much closer to the original.
    - Saturator changed to better emulate SQ80 at ORIG setting.
    - DCA1-3 volume curves changed.
    - Fixed bug with restarting of envelopes.
    - Fixed some LCD updating problems.
    - Changed keyboard capturing mechanism (for entering sound names).
    - Added the parameters saturation and envelope 4 amount to the
      MIX page.
    - Sound program names should now be correctly converted from/to
      SysEx.
    - New LCD and other changes in GUI design.
    
  --- 0.831 alpha -------------------------------------------------

    - Fixed problem with LCD updating using Ableton Live.

  --- 0.83 alpha --------------------------------------------------

    - The windows registry is no longer used to store plugin paths
      and settings and no installer is needed.
    - Fixed problem with reading write protected files.

  --- 0.82 alpha --------------------------------------------------

    - Fixed problem with dialog windows. Now they should be displayed
      correctly not showing on the task bar.
    - Fixed wrong placement of GUI components inside the window when
      the windows task bar is placed on the left or on top of the
      screen.
    - Fixed bug which could cause high CPU load when using low
      oscillator volumes (DCA1-3).
    - Fixed another bug causing high CPU load with low final volume.
    - Fixed bug in MIDI processing. There should be less (or no)
      hanging notes now.
    - Sounds fade out more smoothly at the end of the release time.
    - The sound selection window has been replaced by a popup menu.
    - The LFO parameter RESET now allows specifying the start
      phase.
    - The mouse cursor jumps back to previous position after closing
      popup menus or turning knobs (see below "E. The user interface").

  --- 0.81 alpha --------------------------------------------------

    - Smoother modulation of oscillator volumes (including AM mode).
    - Removed clicks in legato playing.
    - Slightly reduced aliasing.

  --- 0.8 alpha ---------------------------------------------------

    - First release.



+-=== D. Synthesis ================================================-+


  This section is meant for users who are already familiar with the
  SQ80/ESQ1. For detailed information on these synths please refer
  to their manuals. The ESQ1 manual can be found on Rainer Buchty's
  page:
    http://www.buchty.net/

  In the SQ8L the following things have been added to the SQ80
  features or changed:

     - The scrollable page OSC1-3 Mix/Waves/Tune allows quick access
       to each oscillator's pitch, waveform and volume. In addition
       the global parameters FINAL (final volume), SAT (saturation
       amount), SYNC and AM can be edited here.

     - Additional LFO4 and several new features (see paragraph D.2).

     - Additional envelope features (see paragraph D.3).

     - All MIDI controllers are available as modulation sources.

     - Freely assignable modulator for the final volume.

     - 3 Matrices (MAT1, MAT2, MAT3) as new modulation sources
       which are the sum of up to 3 other modulators (M1, M2, M3).
       The output amplitude of a matrix can be modulated by another
       modulator (AMP).

     - The range of the filter modulation amount has been doubled
       compared to SQ80/ESQ1 (-127..+127 instead of -63..+63).
       The range -63..+63 matches with the SQ80/ESQ1.

     - The oscillator pitch parameters SEMI and FINE can have
       negative values.

     - The panning range is -63..+63 instead of 0..15.
       The range of the panning modulation amount has been doubled
       compared to SQ80/ESQ1 (-127..+127 instead of -63..+63).
       The range -63..+63 matches with the SQ80/ESQ1.

     - SYNC and AM can be used together.

     - The page DCA4 contains the additional parameter SAT = amount
       of saturation (distortion).
       The purpose of the saturator is to imitate the distortion that
       occurs in the SQ80/ESQ1's analog circuits when setting the oscillator
       volumes to high values. The saturation is applied after the filter.

     - The following midi controllers are always recognized:
          7 (07 hex) : Master volume
         10 (0A hex) : Panning (relative, 64=neutral)
         11 (0B hex) : Expression (relative volume increase,
                       0=neutral)*
         64 (40 hex) : Hold/Sustain pedal (values>0 = hold notes)**
         74 (4A hex) : Brightness (relative filter frequency,
                       64=neutral)*

         *  May have little or no effect depending on the
            corresponding parameter settings and modulation.

         ** Has no effect if the sustain stage of the envelopes
            is disabled (CYC=ON on the MODE page).



  --- D.1. Emulation parameters -------------------------------------


  The emulation page (EMU) contains the following parameters
  which are NOT global, but stored with each sound:

    - BEND = pitch bend range (semitones)

    - MODE selects which notes are affected by pitch bend.
       Possible values are:
         ALL = all notes
         HELD = only held (sustained) notes
         NEW = only the newest note
         NEWH = only the newest held note
         HELD2, NEW2, NEWH2 = like above, but if the affected
           note changes, the old one "forgets" the pitch bend
           and returns to normal pitch.

    - AMBUG switches the emulation of a bug in the SQ80 on
       and off. Sounds using AM=ON together with one-shot
       waveforms are affected.

    - VSTEAL selects the voice stealing mode.
       Possible values are:
         HARD = stolen voices are immediately stopped resulting
           in audible clicks.
         SOFT = fade out voices softly. In the worst case this
           can take as much CPU time as 16 voices playing.

       The VSTEAL parameter can be globally overridden (for
       all SQ8L instances) with the "Voice stealing mode..."
       setting in the options menu.
       The default is SOFT (overriding the VSTEAL parameter in
       sound programs).

       Note: Only up to 8 voices can be fading out at any time.
       Playing too many notes together may produce audio clicks
       regardless of the used voice stealing mode!


  The following parameters are used to better emulate the SQ80/ESQ1.
  However, they may have little or no audible effect depending
  on the current sound program.
  Any of these parameters can be globally overridden by setting
  the corresponding entry in the "Options->Emulation..."
  menu to a value other than "Set by program".

    - SMOOTH-DCA1-3 selects between two modes of smoothing the
       oscillator volumes:
         EMU = tries to emulate the SQ80/ESQ1's smoothing accurately,
           but causes some latency in the modulation of the
           volumes.
         FAST = less accurate, but without latency.

    - SMOOTH-DCA4 controls smoothing of the final volume:
         EMU = emulate the SQ80's limited steepness of the attack
           stage of envelope 4. If the envelope's attack time T1
           is less then 3, the attack will be slightly steeper
           than with the SQ80/ESQ1.
         HARD = allow really steep attack for envelope 4.
           T1 values for envelope 4 less than 3 may result in audible
           clicks. The HARD setting is suitable for percussive
           sounds.

    - MUFFLE: If switched ON, high frequencies of the SQ8L's overall
       output are attenuated to produce a warmer, less digital sound
       (more like the SQ80/ESQ1). Leave it switched OFF for a crispier
       sound.

    - DC-BLOCK: The oscillator's mixed output is filtered to block
       DC (=Direct Current) offsets.
       Signals with a DC offset are not symmetrically oscillating
       around zero level but around the DC level instead. If multiple
       such signals are mixed together their DC levels add up too, which
       in most cases will cause serious problems in further audio
       processing (e.g. effects).
       Using oscillator 2 synchronization (SYNC=ON) may result in
       considerable DC offsets.
       The settings of the DC-BLOCK parameter are:
         SMART = DC blocking is only used when needed. In the current
           SQ8L version DC blocking is turned on if oscillator 2
           sync is used (SYNC=ON).
         ON = DC blocking is always active.
         OFF = DC blocking is always turned off.


  --- D.2. Extended LFO features ------------------------------------


  - The frequency range has been extended from 0..63 to 0..127 (0..63
    matches with SQ80/ESQ1).

  - The amount of LFO amplitude modulation is adjustable.

  - The RESET parameter of the LFOs can be switched to OFF or
     set to a start phase.

  - Extended humanization (HUMAN) modes:
      OFF = no humanization
      ON = emulate the SQ80/ESQ1's humanization:
            In this mode humanization is disabled for LFO frequencies
            below 7 and during delay.
      1x = humanization is alway active.
      2x, 4x, 8x, 16x = the LFO frequency is randomized 2, 4, 8 or 16
                         times as much.

  - New LFO waveforms:
      - BIP: Bipolar rectangle wave (alternating between positive and
              negative values).
      - 00..69: Wavetables normally used by the main oscillators.
      - EXP..EXP4: Exponential shaping tables with increasing steepness.
      - TAN..TAN4: Tanh (hyperbolic tangent) shaping tables
                    with increasing steepness.


  Each LFO's sub-page shows the following parameters:

  - FREQMOD allows to select a modulator for the LFO's frequency
     (if FM=UNI or FM=BIP, see below).
     Note: If the frequency becomes negative through modulation the
            LFO's playback direction will be reversed!

  - PHS allows adjusting the phase offset of the LFO. This is
     independent of the RESET paremeter. Values with a "T" indicate
     use of the Twin mode:
      In Twin mode, a 2nd phase-shifted instance of the same waveform
      is subtracted from the first one (which has a zero phase offset).
      The phase shift between the two waves is controlled by the value
      of the PHS parameter.

  - SMTH controls smoothing of the LFO's wave. If SMTH=00 the waveform
     is left unchanged. Please note that high values will reduce the
     LFO's amplitude significantly. Thus, modulating the smoothness may
     be good alternative to modulating the amplitude.

  - MODE-DELAY switches between two LFO delay (=fading) modes:
      EMU = emulate the SQ80/ESQ1's very coarse fading with clearly
             audible steps.
      SMTH = smoother fading.

  - MODE-AM, MODE-FM selects between different modes for the amplitude
     modulator (MOD) and the frequency modulator (FREQMOD):
       UNI = unipolar modulation: The modulating signal is clipped
              to provide only positive values. The SQ80/ESQ1 use this
              for amplitude modulation.
              Note: The modulation amount may still be negative!
       BIP = bipolar modulation: The modulation source is not clipped.
              Earlier versions of the SQ8L incorrectly used this for
              amplitude modulation.
       PHS = Instead of the LFO's amplitude or frequency, its phase
              offset (PHS) is modulated. In Twin mode, the phase shift
              between the two waves is modulated.
       SMT = Instead of the LFO's amplitude or frequency, its smoothness
              (SMTH) is modulated.

  - MODE-PLAY:
      FWD = forward playback
      REV = reversed (=backwards) playback. The PHS parameter is
             adjusted accordingly.
      1XF = one-shot forward: The waveform is played once forward until
             the end of the waveform is reached.
      1XR = one-shot reversed: The waveform is played once backwards
             until the beginning of the waveform is reached.

      It should be noted that in 1XF and 1XR modes the LFO's phase at
      the time of triggering (which can be set with the RESET parameter)
      controls the length of the played portion of the waveform.
      However, the phase offset (PHS) controls where this portion is
      located within the waveform.

  ... D.2.2. Example: Shaping modulation signals with LFOs ..........

  As an example of how to use the LFOs, let me show you how to use an
  LFO as a nice exponential shaper for an envelope. This can also be
  accomplished using the envelope's SHAPE parameter but using an LFO
  is much more flexible. The LFO settings of interest are:

    FREQ=000, HUMAN=OFF : Keeps the LFO from oscillating.

    RESET=00 : Makes sure the LFO will be reset when the voice is
      triggered.

    WAVE=EXP2 : This wave is suitable for exponential shaping.

    FREQMOD=ENV1 * +064, FM=PHS : Selects the modulation signal to be
      shaped (=the LFO's phase modulator). In this case it's envelope 1.
      The value +064 ensures that the full range of positive and negative
      input values are each mapped to half of the LFO's wave.

    PHS=32 : Positive envelope levels will be shaped using the 2nd
      half of the LFO wave (where the EXP2 wave rises from 0 to 127).
      Negative levels will use the 1st half (EXP2 rises from -128 to -1).

  To make this even more fun, try the following:

    AM=SMT : Use the amplitude modulator slot to modulate the
      smoothness of the LFO's output.

    SMTH=55 : This will make things real smooth.

    MOD=VEL * -63 : The harder you strike a key, the less smooth
      the output will be.

  Now, for example use the LFO to modulate the filter cutoff frequency.
  Note: Selecting SAW in this example as LFO wave would leave the envelope
         or any other input signal unchanged except the smoothing.


  --- D.3. Extended envelope features -------------------------------


  Each envelope's sub-page shows the following parameters:

  - L0: The envelope's start level. In earlier versions of the SQ8L
         as well as the SQ80/ESQ1 this always was fixed to zero level.

  - CYC: Like the CYC parameter on the MODE page this controls wether
          the envelope has a sustain stage or always plays its full
          cycle. But this parameter controls each envelope independently.
          The envelope's CYC parameter is overridden if the global
          CYC parameter on the MODE page is ON.

  - SMTH controls smoothing of the envelope's output. If SMTH=00 the
     smoothing is disabled.

  - MODE-T1V switches between:
      T1 = Velocity modulates attack time (T1) by amount in T1V
      SMT = Velocity modulates smoothness (SMTH) by amount in T1V

  - Different output shapers (SHAPE):
      OFF = no shaping
      EXP..EXP4 = exponential shaping
      TAN..TAN3 = hyperbolic tangent shaping


+-=== E. The user interface =======================================-+



   --- E.1. LCD*, knobs and parameters ------------------------------

   The GUI (graphical user interface) has been designed to recreate
   the look-and-feel of the SQ80. The LCD always displays one page
   which allows accessing some of the sound parameters. The pages
   can be selected with the according buttons or via a popup menu which
   opens on right-clicking almost anywhere on the GUI window.
   Each page contains up to 10 sound parameters which can be edited
   with the corresponding knobs.
   Parameter values can be changed by clicking the knobs or the
   parameter values itself on the LCD with the left mouse button,
   holding it and moving the mouse up and down. Moving the mouse
   left or right away from the position you clicked will make the
   mouse more sensitive.
   Double-clicking a parameter on the LCD or a knob opens a popup
   menu with all possible values or, in case of a binary value,
   toggles between the two possible values (in most cases ON/OFF).
   When moving the mouse cursor over a parameter or knob, a short
   description is displayed at the bottom of the window.

   * In fact, the SQ80's display is not an LCD but a VFD. To avoid
     confusion, I will call it LCD anyway.



   --- E.2. Scrollable pages ----------------------------------------

   Basically, the scrollable pages are groups of individual sub-pages.
   They are used to show additional parameters that would not fit on one
   page (e.g. the LFO pages) or to group pages for quicker access
   (e.g. the Mode/Emulation pages). If the current page can be scrolled
   at least one of the arrows on the right hand side of the display will
   be lit. You can scroll the sub-pages by clicking on those arrows, or
   you can cycle through them by right-clicking on the display (this can
   be disabled with the setting "Right click on display -> scroll page"
   in the OPTIONS menu).



   --- E.3. Page buttons --------------------------------------------

   The parameter pages can also be accessed by clicking on the
   corresponding buttons. If the currently selected page is scrollable
   clicking on its button will cycle through tha page's sub-pages.



   --- E.4. The modulation source usage window ----------------------

   This window can be opened from the INFO menu or the page popup menu.
   It's still just temporary and NOT interactive, but quite helpful.
   All used modulation sources are listed (on the left) with all
   modulated parameters (on the right after "->").



   --- E.5. The "jumping mouse" -------------------------------------

   By default the mouse cursor jumps back to the previous position
   after closing popup menus or turning knobs.
   This may feel a bit strange at first but allows faster editing
   with less mouse movements.
   It can be disabled in the OPTIONS menu ("Mouse position is
   restored after...") for popup menus and knobs separately.



   --- E.6. The sound library ---------------------------------------

   In the latest version an SQ8L library contains 256 user sounds
   organized in two banks "A" and "B". In addition there are two
   write protected factory banks "C" and "D". Bank "C" contains
   128 SQ8L factory sounds. Bank "D" contains the 40 factory sounds
   of the orginal SQ80 in the slots 000 to 039.

   In the FILE menu, the Load/Save/Init Library commands refer to
   the user sounds in banks "A" and "B". Thus, a SQ8L library now
   contains 256 sounds.
   The Load/Save/Init Bank commands in the FILE menu refer to the
   currently selected sound bank. Note, that you can't load anything
   into the factory banks "C" and "D", nor can you initialize them.
   
   The user library is shared among all running SQ8L instances
   (in the same VST host instance).
   The user sounds in the current library are backed up when
   the last SQ8L instance is closed and restored when the first is
   reopened. The file used for this is named "SQ8L_backup.dat" and
   is in fact an ordinary SQ8L library.

   Note: SQ8L versions 0.90b or higher use a new library file format.
     Files from older versions are automatically imported, but
     exporting in the old format is not supported.

   ! Caution: A present "SQ8L_backup.dat" in old format will be
       automatically imported and saved in new format. Currently there
       is no way to convert it back the old format!



   --- E.7. Selecting & writing sounds to the library ---------------

   Above the LCD you'll find a panel containing a text box with the
   name of the sound program currently in the edit buffer.
   Clicking on the arrow buttons* loads the next/previous sound
   from the current sound bank.
   Double-clicking or right-clicking it opens a menu which lets you
   select one of the sounds currently in the library.
   The bank can be selected by clicking the "BANK" button or in the
   sound selection popup menu.
     Caution: An unsaved sound in the edit buffer
              will be lost when switching the bank!
   Left-click on the sound name box to edit it. Press "Enter" or
   click elsewhere on the synth to end editing.
   Click on the "WRITE" button to save the edited sound to the
   library. In the dialog that will open you can select the slot
   in the library to overwrite. If "COMPARE" is checked you can
   play the selected sound stored in the library.
   The "INIT" button initializes the sound in the edit buffer.

   * Hint: The behaviour of the arrow buttons can be changed by
     editing "swapProgUpDn=0" in the file "SQ8L\SQ8L.ini".
     Possible values are:
       "swapProgUpDn=0" : up button=next sound, down=previous
       "swapProgUpDn=1" : up button=previous sound, down=next



   --- E.8. Panic ---------------------------------------------------

   The button "PANIC" resets the synth engine and stops all playing
   voices. Click this if anything goes wrong (hanging notes etc.).



   --- E.9. Exchanging sounds with the real synths ------------------

   The buttons "SEND" and "REQ" (request) are used to exchange sound
   programs with a real SQ80/ESQ1. The first time you click on one of
   these after opening the GUI you are prompted to select the MIDI
   input or output port to which your SQ80/ESQ1 is connected. You can
   also use the corresponding entries in the "FILE" menu which
   always allow you to select the MIDI ports. The SQ80/ESQ1 must
   be set to the MIDI channel "1" for this to work.
     Caution: When exporting sounds for use with the ESQ1 be sure not
              to make any settings the SQ80 does support but the ESQ1
              doesn't!



   --- E.10. The (computer) keyboard capturing ----------------------

   While editing the sound name (the edit box is focused), all
   keystrokes are stolen from the host and other plugins, so that
   even keys are available which normally are hot keys of the host.
   However, the mechanism for detecting when to free the keyboard
   again may be fragile. Therefore, the behaviour can be
   changed by editing the file "SQ8L\SQ8L.ini" and setting
   "keyCaptMode" to any of the following values:
      "=0" : Free keyboard when losing input focus or when a
             standard dialog or menu is opened.
      "=1" : Like "0", but also free keyboard when any window is
             opened (default).
      "=-1" : No keyboard capturing!
   Changes in the SQ8L.ini take effect only after reloading the
   plugin.

   
      
+-=== F. Known problems ===========================================-+

   The current version of SQ8L has the following problems:

      - Bad documentation.
      - Doesn't work with sample rates below 44100 Hz.
      - The saturator doesn't emulate the distortion in the SQ80
        very well. The setting EMU ("original") is not guaranteed
        to produce the "correct" amount of distortion.
        Furthermore, high SAT values will result in aliasing of
        high pitched notes.
      - Playing many notes at the same time may produce clicks.
      - Emulation of the bug in AM mode not correct.
      - Updating the LCD may cause audio clicks.

   Please feel free to report any bugs not yet listed here via Mail!

+-=== G. Things to come... ========================================-+

   The full version SQ8X will have the following additional features:

      - Combinations of up to 4 single sounds.
      - Multi mode with 16 channels.
      - Arpeggiator which allows C64-like chords.
      - Adjustable polyphony (far more than 8 voices).
      - New Filter algorithms with different modes
        (lowpass, bandpass, highpass).
      - 2nd Filter and different routing modes for the
        filters: serial, parallel, split.
      - Improved GUI.

   Note: I know the wait for the SQ8X is getting long. Please be
         patient a little longer. It is definitely planned to be
         released this year!
         And it will contain some nice surprises...

