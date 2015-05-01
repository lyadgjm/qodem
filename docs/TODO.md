Qodem TODO List
===============

NEW FUNCTIONALITY
-----------------

Bug on telnetd: set LANG
Wishlist on ncurses: expose double-width / double-height
Bug on xterm/ncurses: A_BOLD and ACS_VLINE
Bug on xterm: -fbx/+fbx doesn't seem to do anything
Bug on xterm: A_REVERSE + DECSCNM + A_BOLD

BUG: check when phonebook calls start_quicklearn() after either
     net_connect() or for dialup

BUG: with ssh, enter username/password, press ESC, press Enter --> crash

1.0.0
-----

Detect xterm alternate screen and clear scrollback to retain what was
seen before.

SGR mouse reporting

Re-order options to be more reasonable

Q_OPTION_SCRIPTS_DIR

QODEM_USE_SDL chance to Q_SOUND_SDL

New autoconf build:
  Basic working: default builds same as Makefile.generic
  make dist
  --enable-sdl - looks for system libSDL
  --enable-x11 - builds PDCurses X11
  --enable-ssh - builds libz/gpg-error/gcrypt/ssh2
  --enable-upnp - builds miniupnpc

Code sweep:
  80 column max
  Eliminate Borland warnings
  Ensure return codes are actually used, or switch them to void

Win32 port:
  Fix "My Documents" for __BORLANDC__
    Use _("My Documents") since SHGetFolderPath is missing
  zlib
  libgcrypt
  libssh2
  UPnP
  Resizable window
  Terminus font
  Verify SGR colors (brown, bright yellow, etc.)
  Remove Q_PDCURSES_WIN32-only #include's (no more mingw build)
  Switch __BORLANDC__ to Q_PDCURSES_WIN32
    Except for my_swprintf()'s and common.h/common.c
  InnoSetup Windows installer:
    Install Terminus font + qodem executable
    Custom directories:
      working dir
      host dir
      download
      upload dir
      scripts dir
  Borland 5.02 makefile
  Visual C++ build
    Eliminate warnings
  OpenWatcom build
    Eliminate warnings
  Borland 5.5 build
    Eliminate warnings

OS X Build:
  App Icon
  dmg image

FreeBSD build

OpenBSD build

NetBSD build

Minix3 build

Haiku build

RPM build
  Contact Fedora maintainer to sync up qodem.spec and also add
  qodem-x11.spec

Debian build
  Pass lintian
  Apply for Debian maintainer position, or seek willing
  maintainer
  qodem
  qodem-x11


Finish up modem support:
  host.c:
    MODEM answer:
      send host_init_string
      wait for RING
      send answer_string
      check DCD for online


Fix all marked TODOs in code


FULL REGRESSION ON EVERY ITEM:
  F10 -> Enter or Alt-Enter
  F2 -> Space
  Translate tables
    Input
      UTF-8
    Output
      UTF-8
  Keyboard editor
  Keyboard macros
  Modem config
  Serial port settings
  Toggles
    Full duplex
    Strip 8th
    Beeps and bells
    ...
  Split screen
  Scrollback
    View up/down
    Clear
    Save to file
  Screen dump
  List directory
  View file
  View log file
  Send break
  Codepage
  Serial port
    5-bit
    6-bit
    7-bit
    8-bit
    Mark / Space
    RTS/CTS
    XON/XOFF
  Compose key
    8-bit
    Unicode
  Edit options
    Reload options after edit
  Uploads
    ASCII
    Xmodem
    Xmodem CRC
    Xmodem 1k
    Xmodem Relaxed
    Xmodem 1k-G
    Ymodem
    Ymodem G
    Zmodem
    Kermit
  Downloads
    ASCII
    Xmodem
    Xmodem CRC
    Xmodem 1k
    Xmodem Relaxed
    Xmodem 1k-G
    Ymodem
    Ymodem G
    Zmodem
    Kermit
  Script
  Phonebook:
    Find
    Find Again
    Manual Dial
    Delete Tagged
    Sort
    Tag
    Edit Notes
    Edit Script
  Capture
    Raw
    Normal
    Html
  Emulations:
    VT52
    VT100
    VT102
    VT220
    LINUX
    XTERM
    L_UTF8
    X_UTF8
    ANSI
      ANSI music
    AVATAR
      ANSI fallback
        ANSI music
    DEBUG
  Command-line switches:
    --connect
    --connect-method
    --play
    --play-exit
    --dial
    --username

Qodem support BBS:
  BBS with:
    www, ftp, telnet, ssh
    x/y/zmodem, kermit
    long filenames (?)
  File boards:
    Qodem Releases
    Qodem Scripting
    Qmodem(tm)
    Other Communication Programs
    Offline Mail Readers
    Terminal Emulation
    File Transfer Protocols
    Linux
    DOS
  Message bases:
    Qodem Support
  Link to Fidonet
  Link to DOVE-Net
  Regular BBS ad announcement


Release:
  Eliminate DEBUG_*, // comments
  Update ChangeLog
  #define RELEASE common.h
  Update Telnet BBS List
  Check dates on web pages:
    index.html screenshots.html getting_started.html
  Sync up text in help.c and man pages and README
  Rebuild man page HTML:
    groff -mandoc `man -w docs/qodem.1` -T html > qodem.1.html
  Copy qodem.1 -> qodem-x11.1
    Change qodem -> qodem-x11 in man page title
    Change xqodem -> qodem in "See Also" section
  Version in:
    FILE_ID.DIZ
    configure.ac
    common.h
    colors.c
    qodem.c
    build/win32/resources.rc
    build/debian/qodem/debian/changelog
    build/debian/qodem/debian/control
    build/debian/qodem-x11/debian/changelog
    build/debian/qodem-x11/debian/control
    build/qodem.spec
    build/qodem-x11.spec
  Update copyrights to current year:
    All code headers
    qodem.c --version
    console.c terminal header
  .tar.gz Source
  Binary builds:
    Fedora i386
    Fedora x86_64
    X11 Fedora i386
    X11 Fedora x86_64
    Debian stable i386
    Debian stable x86_64
    X11 Debian stable i386
    X11 Debian stable x86_64
    MacOS
    Win32
    Win64
  Upload to SF



1.1.0
-----

Full recognition of XTERM sequences

Use puttygen'd keys for ssh

Kermit:
  Locking shift

Win32 port:
  SDL sound
  Serial port support via TAPI
    tcsendbreak - console.c
    open_serial_port
    configure_serial_port
    close_serial_port
    Make serial port field in modem_config pull up a list from TAPI

Send Wake-On-LAN packet to phonebook entry

Automatic virus scanning / post-processing of downloaded files
  UUDECODE/UUENCODE/yEnc/Base64 decoding in ASCII file transfers:
    yydecode
  Virus scan everything:
    clamav
  Generic post processor:
    Session log event: "Spawning file post-processor..."

Direct proxy support (both HTTP and SOCKS)

VT220 printer support

VT52 HOLD SCREEN mode

External protocols

Encrypted phonebook



"MAYBE" / WISHLIST FEATURES
---------------------------

Pacing character support

Autotrigger macros (ala ACECOMM)

PETSCII

ATASCII

Integrate with I2P

Kerberos

HS/Link protocol

Multi-line customizable status display

Encrypted telnet

True telnet NVT ASCII console (linemode option)

"Server Cmds" command menu: telnet, kermit server, PPP
  Be able to sever a Kermit server/PPP link
  Send the other telnet commands (IP, GA, ...)

Intellisense-style completion window:
  Alt-Space?

Parse current command line, figure out what's going on, pop up what?
  Man page?  Alternate arguments?

Copy and paste?

.qwk downloads -> ~/mmail/down
  Detect in zmodem, ymodem, and kermit

IEMSI login and mail transfer

Other emulations:
  SCOANSI
  Wyse50
  Wyse60
  IBM 3270

Session log in w3c/IIS format (for standardized recording of file transfers)

Script library (see Intellicomm)
  Unix login
  Unix SOUP mail download/upload
  Wildcat BBS login, filelist
  SSH through firewall, transfer files, disconnect
  Tradewars 2002 scripts

True native (not PDCurses) port to X11:
  Draw VTxxx fonts graphically (including VT52 chars not in Unicode)
  Sixel graphics
  ReGIS graphics
  Tektronix

SPINOFFS
--------

Drop-in replacement for lrzsz that does better error checking

Re-license XYZmodem + Kermit implementation as BSD for inclusion in
other projects: PuTTY

Linux/ncurses port of HS/Link 1.21

QUESTIONS TO ASK OUT THERE
--------------------------