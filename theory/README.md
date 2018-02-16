# Theory of Computation Sprint Challenge

## Regular Expressions

Find regexes that match the following. (e.g. find a single regex that matches
both `antelope` and `antelopes`.)

* Single regex that matches either of these:

    antelope rocks out
    antelopes rock out

    answer: /(antelope | antelopes)/g

* Regex that matches either of:

    goat
    moat

  but not:

    boat

    answer: /([g|m]oat)/g

* Regex that matches dates in YYYY-MM-DD format. (Year can be 1-4 digits, and
  month and day can each be 1-2 digits). This does not need to verify the date
  is correct (e.g 33333-33-33 can match).

  2000-10-12
  1999-1-20
  1999-01-20
  812-2-10

  answer: /[\d]{4}-[\d]{1,2}-[\d]{1,2}/g

## State Machines

> A useful tool for drawing state machines is [Evan's FSM
> Designer](http://madebyevan.com/fsm/).

* Draw a state machine that corresponds to the following regex:

      ab*c+d?[ef]

  Remember the ε transition can be used to move between states without
  consuming input. 

  S0: a
  S1: b or epsilon (0 b's or more)
  S2: c (1 c or more)
  S3: d or epsilon (0 or 1 d, not more)
  S4: e xor f
  S5: final

* A lion can be sleeping, eating, hunting, or preening. Draw a state
  machine diagram for the lion and label the transition events that
  cause state transitions.

  S0: sleeping
    case: is hungry
      state: 1 hunting
    case: pride has food
      state: 2 eating
    case: potential mate near
      state: 3 preening
  
  S1: hunting
    case: unsuccessful hunt
      state: 0 sleeping
    case: makes kill
      state: 2 eating
    case: gives kill to pride
      state: 3 preening

  S2: eating
    case: food coma
      state: 0 sleeping
    case: still hungry
      state: 1 hunting
    case: got dirty
      state: 3 preening

  S3: preening
    case: end of day
      state: 0 sleeping
    case: easy kill near
      state: 1 hunting
    case: pride returns with food
      state: 2 eating

* The VT-100 terminal (console) outputs text to the screen as it
  receives it over the wire. One exception is that when it receives an
  ESC character (ASCII 27), it goes into a special mode where it looks
  for commands to change its behavior. For example:

      ESC[12;45f

  moves the cursor to line 12, column 45.

      ESC[1m

  changes the font to bold.


  move cursor: /ESC\[([\d]{2});([\d]{2})f/g
  make bold: /ESC\[1m(\w)+/g

  state 0: incoming characters
    case: escape to move cursor
      state: 1 parse two sets of digits to correlate row and column
    case: escape to bold
      state: 2 parse 1m to indicate bold font

  * Come up with regexes for the two above sequences. The one to set the
    cursor position should accept any digits for the row and column. The
    bold sequence need only accept `1` (and is a trivial regex). (ESC is
    a single character which can be represented with `\e` in the regex.)

  * Draw a state machine diagram for a VT-100 that can consume regular
    character sequences as well as the two above ESC sequences.

> If you're curious, [here are all the VT-100 escape
> sequences](http://ascii-table.com/ansi-escape-sequences-vt-100.php).
> More common these days is a superset of VT-100 called [ANSI escape
> sequences](http://ascii-table.com/ansi-escape-sequences.php). If
> you've ever put colors and stuff in your Bash prompt, this is what you
> used to do it.
>
> One of your instructors was once hired to implement VT-100 emulation
> in an app, and they used a state machine to do it.
