swaynagmode
-----------
```
swaynagmode
v0.2.1
github.com/b0o/swaynagmode

A wrapper script which provides programmatic control
over swaynag, intended for use with keyboard bindings.

To create a nag, simply use swaynag options as normal - they will be parsed and passed through.

To customise a nag, use these additional options:

  short      long           description
  -M <mode>  --mode         name of sway mode to trigger on init (default: nag)
                            NOTE: beginning in sway version 1.2, mode names are case-sensitive
  -D <mode>  --mode-default name of sway mode to trigger on exit (default: default)
             --no-mode      disable triggering of sway modes
  -i <index> --initial      index of the initially selected button (default: 0)
  -K         --no-kill      don't add a kill command to the button actions
  -R         --reverse      reverse the button order

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
  -h     --help     display usage information for swaynagmode and swaynag
  -H     --help-snm display usage information for swaynagmode
  -v     --version  output version

Caveats:
  - Only one instance of swaynagmode may be run at a time.

Example sway configuration:

  # nag
  set {
    $nag         exec swaynagmode
    $nag_exit    $nag --exit
    $nag_confirm $nag --confirm
    $nag_select  $nag --select
  }
  mode "nag" {
    bindsym {
      Ctrl+d    mode "default"

      Ctrl+c    $nag_exit
      q         $nag_exit
      Escape    $nag_exit

      Return    $nag_confirm

      Tab       $nag_select prev
      Shift+Tab $nag_select next

      Left      $nag_select next
      Right     $nag_select prev

      Up        $nag_select next
      Down      $nag_select prev
    }
  }
  bindsym {
    $super+Shift+q $nag -t "warning" -m "Exit Sway?" -b "Exit" "swaymsg exit" -b "Reload" "swaymsg reload"
  }
  # -R is recommended for swaynag_command so that, upon a syntax error in your sway config, the
  # 'Reload Sway' option will be initially selected instead of the 'Exit Sway' option
  swaynag_command $nag -R


(c) 2019-2021 Maddison Hellstrom <github.com/b0o>

GPL License (https://www.gnu.org/licenses/gpl-3.0.txt)
```
