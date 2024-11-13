Quality of Life features
########################


Before we start, let's install some quality-of-life features to improve the user experience.

.. code-block:: console

   $ sudo apt install -y zsh git curl wget byobu vim\
   && sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

Choose :code:`zsh` as default by hitting enter.

.. code-block:: console

   $ mkdir -p "$HOME/.zsh" && \
   git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure" && \
   echo 'fpath+=$HOME/.zsh/pure \nautoload -U promptinit; promptinit \nprompt pure' | cat - ~/.zshrc > temp && mv temp ~/.zshrc && \
   sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME=""/' ~/.zshrc && \
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && \
   sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions)/' ~/.zshrc && \
   echo "zstyle ':prompt:pure:path' color 075\nzstyle ':prompt:pure:prompt:success' color 214\nzstyle ':prompt:pure:user' color 119\nzstyle ':prompt:pure:host' color 119\nZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=161'" >> ~/.zshrc && \
   echo "zstyle ':prompt:pure:path' color 075\nzstyle ':prompt:pure:prompt:success' color 214\nzstyle ':prompt:pure:user' color 119\nzstyle ':prompt:pure:host' color 119\nZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=161'" >> ~/.zshrc && \
   echo "export TERM=xterm-256color" >> ~/.zshrc && \
   source ~/.zshrc && \
   byobu-enable




Useful Shortcuts for Byobu
--------------------------

.. table::
   :widths: 5 15

   +--------------------------------------------------------+------------------------------------------------------------------+
   | Shortcut                                               | Function                                                         |
   +========================================================+==================================================================+
   |                        :kbd:`F2`                       | Open new terminal window                                         |
   +--------------------------------------------------------+------------------------------------------------------------------+
   |                        :kbd:`F3`                       | Move to previous window                                          |
   +--------------------------------------------------------+------------------------------------------------------------------+
   |                        :kbd:`F4`                       | Move to next window                                              |
   +--------------------------------------------------------+------------------------------------------------------------------+
   |                        :kbd:`F6`                       | Detach from this session                                         |
   +--------------------------------------------------------+------------------------------------------------------------------+
   | :kbd:`Ctrl` + :kbd:`A` and then :kbd:`Ctrl` + :kbd:`D` | Also Detach from this session.                                   |
   |                                                        |                                                                  |
   |                                                        | The first time you use this, you will be asked whether you       |
   |                                                        |                                                                  |
   |                                                        | want to use *screen* hotkeys or *emacs* hotkeys. Choose screen.  |
   +--------------------------------------------------------+------------------------------------------------------------------+
   |                 :kbd:`Alt` + :kbd:`F12`                | Turn mouse support for scrolling on/off                          |
   +--------------------------------------------------------+------------------------------------------------------------------+

Here's a more elaborate `cheat sheet <https://gist.github.com/inhumantsar/bf86ff1961cccdf8be06>`_.
