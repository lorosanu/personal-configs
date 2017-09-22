
# Sublime-Text-3 installation for multiple desktop workspaces

* set apps locations

    ```
    USERAPPS="/usr/share/applications/"
    LOCALAPPS="${HOME}/.local/share/applications/"
    ```

* uninstall any previous version of sublime

    ```
    sudo dpkg -r sublime-text
    sudo rm -rf /opt/sublime_text*
    sudo rm -rf /bin/subl*
    sudo rm -f $USERAPPS/sublime.desktop
    sudo rm -f $LOCALAPPS/sublime.desktop
    sudo rm -rf ~/.config/sublime-text*
    ```

* [install sublime](http://tipsonubuntu.com/2017/05/30/install-sublime-text-3-ubuntu-16-04-official-way/)

    ```
    # install apt-transport-https pkg if missing
    sudo apt-get install apt-transport-https ca-certificates

    wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
    echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
    sudo apt-get update
    sudo apt-get install sublime-text
    ```

* copy run_sublime script under $USERAPPS and use it as sublime's executable

    ```
    # install wmctrl (window manager tool) if missing
    sudo apt-get install wmctrl

    sudo cp run_sublime $USERAPPS
    sudo chmod +x ${USERAPPS}/run_sublime

    sudo sed -e "s~Exec=.* ~Exec=${USERAPPS}/run_sublime ~" -i ${USERAPPS}/sublime_text.desktop
    ```

* use a base16 color scheme

    ```
    wget https://raw.githubusercontent.com/pgaspar/base16-eighties-dark/master/base16-eighties-dark.tmTheme
    sudo mkdir -p ~/.config/sublime-text-3/Packages/User/
    cp base16-eighties-dark.tmTheme ~/.config/sublime-text-3/Packages/User/
    ```

* set user preferences

    ```
    cp Preferences.sublime-settings ~/.config/sublime-text-3/Packages/User/
    cp Python.sublime-settings ~/.config/sublime-text-3/Packages/User/
    cp Markdown.sublime-settings ~/.config/sublime-text-3/Packages/User/
    ```

* show preferences
    - global

        ```
        {
          "close_windows_when_empty": true,
          "color_scheme": "Packages/User/base16-eighties-dark.tmTheme",
          "default_encoding": "UTF-8",
          "default_line_ending": "unix",
          "ensure_newline_at_eof_on_save": true,
          "font_size": 10,
          "hot_exit": false,
          "ignored_packages":
          [
            "Package Control",
            "Vintage"
          ],
          "remember_open_files": false,
          "rulers":
          [
            80
          ],
          "tab_size": 2,
          "translate_tabs_to_spaces": true,
          "trim_trailing_white_space_on_save": true,
          "update_check": false
        }
        ```

    - for Python

        ```
        {
          "tab_size": 4
        }
        ```

    - for Markdown

        ```
        {
          "tab_size": 4,
          "trim_trailing_white_space_on_save": false
        }
        ```
