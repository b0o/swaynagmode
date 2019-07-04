swaynagmode
-----------
```
v0.1.0
github.com/b0o/swaynagmode

A wrapper script which provides programmatic control
over swaynag, intended for use with keyboard bindings.

To create a nag, simply use swaynag options as normal - they will be parsed and passed through.

To customise a nag, use these additional options:

  short      long           description
  -M <mode>  --mode         name of sway mode to trigger on init (default: Nag)
  -D <mode>  --mode-default name of sway mode to trigger on exit (default: Default)
             --no-mode      disable triggering of sway mode
  -i <index> --initial      index of the initially selected button (default: 0)
  -K         --no-kill      don't add a kill command to the button actions

To control an existing nag, use the following options:

  short           long       description
  -x              --exit     dismisses the nag without performing any actions
  -S <prev|next>  --select   selects the previous/next button, wrapping around each end
                             (as specified in arguments left to right, buttons appear from right to
                             left)
  -C              --confirm  accepts the selected button (indicated with [brackets]) and executes its
                             action.

Global options:
  short  long       description
  -h     --help     display usage information
  -v     --version  output version

Example sway configuration:

  # keys
  set {
    $super Mod4
    $meta  Mod1
    $ctrl  Ctrl

    $left  h
    $down  j
    $up    k
    $right l
  }
  # nag
  set {
    $nag         exec swaynagmode
    $nag_exit    $nag --exit
    $nag_confirm $nag --confirm
    $nag_select  $nag --select
  }
  mode "nag" {
    bindsym {
      $ctrl+c   exec $nag_exit
      q         exec $nag_exit
      Escape    exec $nag_exit

      Return    exec $nag_confirm

      Tab       exec $nag_select prev
      Shift+Tab exec $nag_select next

      $left     exec $nag_select next
      $right    exec $nag_select prev

      Left      exec $nag_select next
      Right     exec $nag_select prev

      $up       exec $nag_select next
      $down     exec $nag_select prev

      Up        exec $nag_select next
      Down      exec $nag_select prev
    }
  }
  bindsym {
    $super+Shift+q $nag -t "warning" -m "Exit Sway?" -b "Exit" "swaymsg exit" -b "Reload" "swaymsg reload"
  }

(c) 2019-2019 Maddison Hellstrom <github.com/b0o>

GPL License (https://www.gnu.org/licenses/gpl-3.0.txt)

---

swaynag help:
see swaynag(1) for swaynag usage
```
