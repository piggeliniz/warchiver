#!/bin/bash
##################################################################################
##### LICENSE ####################################################################
##################################################################################
####                                                                          ####
#### Copyright (C) 2018 wuseman <info@sendit.nu>                              ####
####                                                                          ####
#### This program is free software: you can redistribute it and/or modify     ####
#### it under the terms of the GNU General Public License as published by     ####
#### the Free Software Foundation, either version 3 of the License, or        ####
#### (at your option) any later version.                                      ####
####                                                                          ####
#### This program is distributed in the hope that it will be useful,          ####
#### but WITHOUT ANY WARRANTY; without even the implied warranty of           ####
#### MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the            ####
#### GNU General Public License at <http://www.gnu.org/licenses/> for         ####
#### more details.                                                            ####
####                                                                          ####
##################################################################################
##### GREETINGS ##################################################################
##################################################################################
####                                                                          ####
#### To all developers that contributes to all kind of open source projects   ####
#### Keep up the good work!                                                   #<3#
####                                                                          ####
#### https://sendit.nu & https://github.com/wuseman                           ####
####                                                                          ####
##################################################################################
#### DESCRIPTION #################################################################
##################################################################################
####                                                                          ####
#### A friend asked me to fix a tool to sort scene releases from incoming     ####
#### sections into archive dirs wich is sorted with _productname, the paths   ####
#### in preview video is not REAL it's just empty folders for preview         ####
#### how the tool works, don't blame me ;)                                    ####
####                                                                          ####
#### Enjoy another awesome 'bash' script from wuseman. Questions? Conact me!  ####
####                                                                          ####
##################################################################################
#### Begin of code  ##############################################################
##################################################################################


# SETTINGS
section="/volume1/site/software/"

############################################################################
#                                                                          #
# DO NOT TOUCH ANYTHING BELOW UNLESS YOU KNOW EXACTLY WHAT YOU ARE DOING,  #
# THERE MIGHT BE RISKS SINCE IT CAN ERASE UNWANTED DATA                    #
#                                                                          #
############################################################################
ls $section | grep [A-Z] > /tmp/all_releases

create_paths() {
cd $section
ls $section | grep [A-Z] | tr [:upper:] [:lower:] | sed 's/_/./g' | sed 's/-/./g' | awk -F'.' '{print $1}' | sed 's/^/_/g' | sort | uniq | head -n 1 > /tmp/create_dirs
ls $section | grep [A-Z] | tr [:upper:] [:lower:] | sed 's/_/./g' | sed 's/-/./g' | awk -F'.' '{print $1}' | sed 's/^/_/g' | xargs mkdir -p
target="$(cat /tmp/create_dirs | head -n 1)"
source="$(cat /tmp/create_dirs | head -n 1)"
#echo -e "\nCreated a new folder: \e[1;32m$(cat /tmp/create_dirs)\e[0m\n"
}


grab_releases_to_move() {
ls $section | grep [A-Z] | awk -F'.' '{print $1}' | sort | uniq | head -n 1 > /tmp/releases 2> /dev/null
releases="$(cat /tmp/releases | head -n 1)"
}

move_release() {
releases_to_send="$(cat /tmp/all_releases | grep ^$releases)"

#if [ -d "$releases_to_send" ]; then 
#echo -e "\nRelease already exist, moving on..\n"
#rm -rf $releases_to_send
#fi
mv $releases_to_send ./$(cat /tmp/create_dirs)/
echo -e "\e[0;1m[+]\e[0m \e[1;32mRESORTING:\n\e[0m\e[0m\e[1;33m$(cat /tmp/all_releases | grep ^$(cat /tmp/releases))\e[0m \e[1;34 \e[0;1---->\e[0m \e[0m\e[1;32m$(pwd)/$(cat /tmp/create_dirs)\e[0m "

#echo "--------------------------------------------------------------------------------------------"
}

create_paths
grab_releases_to_move
move_release
exit

# Is this needed?
rm /tmp/create_dirs
rm /tmp/create_dirs/underscore
rm /tmp/releases
exit
