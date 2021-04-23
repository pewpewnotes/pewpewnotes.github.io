*boxdraw.txt* A Vim plugin for drawing ASCII diagrams

INTRODUCTION                                    *boxdraw*

The vim-boxdraw plugin makes it easy to draw simple ASCII diagrams in
|blockwise-visual| mode. The basic idea is simple:

- Select a rectangle on the screen
- Invoke a draw command.
  
All commands are mapped to the `+` prefix. See |boxdraw-mappings| for details.

DRAWING RECTANGLES                              *boxdraw-rectangles*

                                                *boxdraw-+o*
+o                      Draw a rectangle, clear its contents with whitespace.

                                                *boxdraw-+O*
+O                      Draw a rectangle, fill it with a label.

                                                *boxdraw-+c*
+c                      Fill the rectangle with a label.

DRAWING LINES                                   *boxdraw-lines*

The following commands draw a one-segment or two-segment line. A simple way
to memorize the mappings:

- Select a rectangle in |blockwise-visual| mode. The line will always go from
  the start corner to the end corner.
- Press `+` and the character that you want to end the line with. vim-boxdraw
  will figure out whether the line should be vertical-horizontal or
  horizontal-vertical, and which direction the arrow should go.
- Press `+` twice if you want to make an arrow on both sides of the line.

See the examples below for full reference. 1 and 2 indicates the start/end
position of the selection.

                                           *boxdraw-+-* *boxdraw-+_*
+- or +_                Draw a line that ends with a horizontal line:

                        1.......    |.......     2.......    -------+
                        ........ => |.......     ........ => .......|
                        .......2    +-------     .......1    .......|


                        .......2    +-------     .......1    .......|
                        ........ => |.......     ........ => .......|
                        1.......    |.......     2.......    -------+


                        ........    ........     ........    ........
                        1......2 => --------     2......1 => --------
                        ........    ........     ........    ........

                                           *boxdraw-+>* *boxdraw-+<*
+> or +<                Draw a line that ends with a horizontal arrow:

                        1.......    |.......     2.......    <------+
                        ........ => |.......     ........ => .......|
                        .......2    +------>     .......1    .......|

                        .......2    +------>     .......1    .......|
                        ........ => |.......     ........ => .......|
                        1.......    |.......     2.......    <------+

                        ........    ........     ........    ........
                        1......2 => ------->     2......1 => <-------
                        ........    ........     ........    ........

                                           *boxdraw-++>* *boxdraw-++<*
++> or ++<              Draw a line that ends with a horizontal arrow,
                        and has an arrow on both sides of the line:

                        1.......    ^.......     2.......    <------+
                        ........ => |.......     ........ => .......|
                        .......2    +------>     .......1    .......v

                        .......2    +------>     .......1    .......^
                        ........ => |.......     ........ => .......|
                        1.......    v.......     2.......    <------+

                        ........    ........     ........    ........
                        1......2 => <------>     2......1 => <------>
                        ........    ........     ........    ........

                                                *boxdraw-+|*
+|                      Draw a line that ends with a vertical line:

                        1.......    -------+     2.......    |.......
                        ........ => .......|     ........ => |.......
                        .......2    .......|     .......1    +-------


                        .......2    .......|     .......1    +-------
                        ........ => .......|     ........ => |.......
                        1.......    -------+     2.......    |.......


                        1.......    |.......     2.......    |.......
                        ........ => |.......     ........ => |.......
                        2.......    |.......     1.......    |.......


                                    *boxdraw-+^* *boxdraw-+v* *boxdraw-+V*
+^, +v or +V            Draw a line that ends with a vertical arrow.

                        1.......    -------+     2.......    ^.......
                        ........ => .......|     ........ => |.......
                        .......2    .......v     .......1    +-------


                        .......2    .......^     .......1    +-------
                        ........ => .......|     ........ => |.......
                        1.......    -------+     2.......    v.......


                        1.......    |.......     2.......    ^.......
                        ........ => |.......     ........ => |.......
                        2.......    v.......     1.......    |.......

                                  *boxdraw-++^* *boxdraw-++v* *boxdraw-++V*
++^, ++v or ++V         Draw a line that ends with a vertical arrow,
                        and has an arrow on both sides of the line:

                        1.......    <------+     2.......    ^.......
                        ........ => .......|     ........ => |.......
                        .......2    .......v     .......1    +------>


                        .......2    .......^     .......1    +------>
                        ........ => .......|     ........ => |.......
                        1.......    <------+     2.......    v.......


                        1.......    ^.......     2.......    ^.......
                        ........ => |.......     ........ => |.......
                        2.......    v.......     1.......    v.......

SELECTING OBJECTS                               *boxdraw-select*

Select commands also work in |blockwise-visual| mode: start a selection,
then press one of the following mappings to select an object:

                                                *boxdraw-+io*
+io                     Select current rectangle, without borders.

                                                *boxdraw-+ao*
+ao                     Select current rectangle, with borders.

https://raw.githubusercontent.com/gyim/vim-boxdraw/master/doc/boxdraw.txt
