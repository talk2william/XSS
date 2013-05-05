#!/bin/bash
#
# XSS : X System Show
#
# Author : Arpan Biswas
# Repo   : https://github.com/talk2william/XSS
#
# **** License ****
#
# The software is distributed under "THE BEER-WARE LICENSE" (Revision 42)
# The Beer-ware license was written by Poul-Henning Kamp. <phk@FreeBSD.ORG>
# ----------------------------------------------------------------------------
# "THE BEER-WARE LICENSE" (Revision 42):
# As long as you retain this notice you
# can do whatever you want with this stuff. If we meet some day, and you think
# this stuff is worth it, you can buy me a beer in return.
# ----------------------------------------------------------------------------
#
# **** variable declaration ****
declaration(){
    # **** color ****
    c0='[0m'
    c1='[1;31m' # RED
    c2='[1;32m' # GREEN
    c3='[1;33m' # YELLOW
    c4='[1;34m' # BLUE
    c5='[1;35m' # PURPLE
    c6='[1;36m' # CYAN
    c7='[1;37m' # GRAY
    c8='[1;30m' # BLACK

    # **** info ****
    OS=$(uname -o)
    HOST=$(hostname)
    USER=$(whoami)

    UPTIME=$(</proc/uptime)
    UPTIME=${UPTIME//.*}
    SECS=$((${UPTIME}%60))
    MINS=$((${UPTIME}/60%60))
    HOURS=$((${UPTIME}/3600%24))
    DAYS=$((${UPTIME}/86400))
    UPTIME="${MINS}m ${SECS}s"
    if [ "${HOURS}" -ne "0" ]; then
  UPTIME="${HOURS}h ${UPTIME}"
	fi
    if [ "${DAYS}" -ne "0" ]; then
	UPTIME="${DAYS}d ${UPTIME}"
	fi

    KERNEL=$(uname -r)
    CPU=$(awk 'BEGIN{FS=":"} /model name/ { gsub(/  +/," ",$2); gsub(/^ /,"",$2); gsub(/\(R\)|\(TM\)/,"",$2); print $2; exit }' /proc/cpuinfo);

    MEM_INFO=$(</proc/meminfo)
    MEM_INFO=$(echo $(echo $(MEM_INFO=${MEM_INFO// /}; echo ${MEM_INFO//kB/})))
    for m in $MEM_INFO; do
	if [[ ${m//:*} = MemTotal ]]; then
	    MEMTOTAL=${m//*:}
	    fi
	if [[ ${m//:*} = MemFree ]]; then
	    MEMFREE=${m//*:}
	    fi
	if [[ ${m//:*} = Buffers ]]; then
	    MEMBUFFER=${m//*:}
	    fi
	if [[ ${m//:*} = Cached ]]; then
	    MEMCACHED=${m//*:}
	    fi
	done
    USEDMEM="$((($MEMTOTAL - $MEMFREE - $MEMBUFFER - $MEMCACHED) / 1024))"
    TOTALMEM="$(($MEMTOTAL / 1024))"
    MEM_DISPLAY="$USEDMEM / $TOTALMEM MB"

    ROOT_USED=$(df -h | grep "rootfs" | cut -d' ' -f14)
    ROOT_TOT=$(df -h | grep "rootfs" | cut -d' ' -f12)
    ROOT_PER=$(df -h | grep "rootfs" | cut -d' ' -f19)
    ROOT_DISPLAY="$ROOT_USED / $ROOT_TOT ($ROOT_PER)"
}

# **** lame quotes ****
lame_quote_gentoo(){
    declare -a arr_gentoo=("Its -O3 the letter, not -03 the number." "Compiling from scratch is really hyped, what makes Gentoo cool is the technical merits like rc-updating and USE flags." "Gentoo does help stop programmers from being lazy, so they write completely airtight code. That can only be a good thing, whichever way you look at it." "What other gnu/linux will let you have a vector optimized wordprocessor?" "Debian is easy to keep up to date. That's because they don't update it." "The performance gained by CFLAGS on x86 is minimal at best -- largely because the machines are still basically overclocked 386's at their core." "HOLY COW I'M TOTALLY GOING SO FAST OH F***!!" "Anyone ever wondered how larry can be a cow!" "If it moves compile it." "I use Gentoo because I'm a speed freak - I can't stand the thought that some of my packages might not be running as fast as they could be.")
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_gentoo[$i]}"
}

lame_quote_dolphin(){
    declare -a arr_world_wars=("Look, good against remotes is one thing, good against the living, that's something else." "Aren't you a little short for a stormtrooper?" "The Force is strong with this one." "I find your lack of faith disturbing." "May the Force be with you." "I'm Luke Skywalker, I'm here to rescue you." "Boring conversation anyway. Luke, we're gonna have company!" "You're all clear, kid! Now let's blow this thing and go home!" "You've never heard of the Millennium Falcon? ... It's the ship that made the Kessel run in less than 12 parsecs." "I am your Father..." )
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_world_wars[$i]}"
}

lame_quote_broken(){
    declare -a arr_world_wars=("I find your lack of faith disturbing." "Luke, I am your father!" "I sense something, a presence I've not felt since......." "You should not have come back!" "The ability to destroy a planet is insignificant next to the power of the force." "Just for once, let me look at your face with my own eyes." "Obi-Wan has taught you well." "He will join us or die, my master." "You have controlled your fear. Now, release your anger. Only your hatred can destroy me." "When I left you I was but the learner. Now I am the master.")
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_world_wars[$i]}"
}

lame_quote_snake_sword(){
    declare -a arr_world_wars=("Fascinating." "Do you want to tell me what's bothering you or would you like to break some more furniture?" "Rumors of my assimilation are greatly exaggerated." "Spock, I do not know too much about these little Tribbles yet, but there is one thing that I have discovered. I like them ... better than I like you." "I would be delighted to offer any advice I can on understanding women. When I have some, I'll let you know." "Do that thing we just talked about." "What does god need with a starship?" "Our neural pathways have become accustomed to your sensory input patterns." "Please, Captain, not in front of the Klingons." "KHAAANNNN!")
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_world_wars[$i]}"
}

lame_quote_cute_bird(){
    declare -a arr_world_wars=("Vengeance will be mine!" "Finish Him!" "Your soul is mine!" "Fatality." "Every man is responsible for his own destiny." "Let the Mortal Kombat begin." "Flawless victory." "Liu Kang Wins!" "Sonya Wins!" "Scorpion and Sub-Zero. Deadliest of enemies but slaves under my power.")
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_world_wars[$i]}"
}

lame_quote_arch(){
    declare -a arr_world_wars=("The interpretation of dreams is the royal road to a knowledge of the unconscious activities of the mind." "The royal road to a man's heart is to talk to him about the things he treasures most." "In the past, people were born royal. Nowadays, royalty comes from what you do." "There was a knight came riding by.. In early spring, when the roads were dry." "A true knight is fuller of bravery in the midst, than in the beginning of danger." "I have played a boxer, a cowboy, a knight, a prince, an elf and a pirate. I am so glad to have done all of that already." "Heroism is endurance for one moment more." "The greatest height of heroism to which an individual, like a people, can attain is to know how to face ridicule." "Faith is the heroism of the intellect." "True heroism is remarkably sober, very undramatic.")
    i=$(expr $RANDOM % 10)
    QUOTE_DISPLAY="${arr_world_wars[$i]}"
}

# **** display ****
display_danger(){
    echo -e "\t\\e${c1}´´´´´´´´´´´´´´´´´´´ ¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶´´´´´´´´´´´´´´´´´´´\`"
    echo -e "\t´´´´´´´´´´´´´´´´´¶¶¶¶¶¶´´´´´´´´´´´´´¶¶¶¶¶¶¶´´´´´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´´¶¶¶¶´´´´´´´´´´´´´´´´´´´´´´´¶¶¶¶´´´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´¶¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´¶¶´´´´´´´´´´´´´´´´´´´´´\`´´´´´´´´´´´¶¶´´´´´´´´´´\`"
    echo -e "\t´´´´´´´´´´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´¶¶´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´¶¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´¶¶´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´¶¶´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´¶¶´´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´¶¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´¶¶´´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´¶¶´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´¶¶´¶¶´´´¶¶¶¶¶¶¶¶´´´´´¶¶¶¶¶¶¶¶´´´¶¶´¶¶´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´¶¶¶¶´¶¶¶¶¶¶¶¶¶¶´´´´´¶¶¶¶¶¶¶¶¶¶´¶¶¶¶¶´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´¶¶¶´¶¶¶¶¶¶¶¶¶¶´´´´´¶¶¶¶¶¶¶¶¶¶´¶¶¶´´´´´´´´´´´´´"
    echo -e "\t´´´´¶¶¶´´´´´´´¶¶´´¶¶¶¶¶¶¶¶´´´´´´´¶¶¶¶¶¶¶¶¶´´¶¶´´´´´´¶¶¶¶´´´"
    echo -e "\t´´´¶¶¶¶¶´´´´´¶¶´´´¶¶¶¶¶¶¶´´´¶¶¶´´´¶¶¶¶¶¶¶´´´¶¶´´´´´¶¶¶¶¶¶´´"
    echo -e "\t´´¶¶´´´¶¶´´´´¶¶´´´´´¶¶¶´´´´¶¶¶¶¶´´´´¶¶¶´´´´´¶¶´´´´¶¶´´´¶¶´´"
    echo -e "\t´¶¶¶´´´´¶¶¶¶´´¶¶´´´´´´´´´´¶¶¶¶¶¶¶´´´´´´´´´´¶¶´´¶¶¶¶´´´´¶¶¶´"
    echo -e "\t¶¶´´´´´´´´´¶¶¶¶¶¶¶¶´´´´´´´¶¶¶¶¶¶¶´´´´´´´¶¶¶¶¶¶¶¶¶´´´´´´´´¶¶"
    echo -e "\t¶¶¶¶¶¶¶¶¶´´´´´¶¶¶¶¶¶¶¶´´´´¶¶¶¶¶¶¶´´´´¶¶¶¶¶¶¶¶´´´´´´¶¶¶¶¶¶¶¶"
    echo -e "\t´´¶¶¶¶´¶¶¶¶¶´´´´´´¶¶¶¶¶´´´´´´´´´´´´´´¶¶¶´¶¶´´´´´¶¶¶¶¶¶´¶¶¶´"
    echo -e "\t´´´´´´´´´´¶¶¶¶¶¶´´¶¶¶´´¶¶´´´´´´´´´´´¶¶´´¶¶¶´´¶¶¶¶¶¶´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´´¶¶¶¶¶¶´¶¶´¶¶¶¶¶¶¶¶¶¶¶´¶¶´¶¶¶¶¶¶´´´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´´´´´´¶¶´¶¶´¶´¶´¶´¶´¶´¶´¶´¶´¶¶´´´´´´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´´´´´¶¶¶¶´´¶´¶´¶´¶´¶´¶´¶´¶´´´¶¶¶¶¶´´´´´´´´´´´´´´"
    echo -e "\t´´´´´´´´´´´´¶¶¶¶¶´¶¶´´´¶¶¶¶¶¶¶¶¶¶¶¶¶´´´¶¶´¶¶¶¶¶´´´´´´´´´´´´"
    echo -e "\t´´´´¶¶¶¶¶¶¶¶¶¶´´´´´¶¶´´´´´´´´´´´´´´´´´¶¶´´´´´´¶¶¶¶¶¶¶¶¶´´´´"
    echo -e "\t´´´¶¶´´´´´´´´´´´¶¶¶¶¶¶¶´´´´´´´´´´´´´¶¶¶¶¶¶¶¶´´´´´´´´´´¶¶´´´"
    echo -e "\t´´´´¶¶¶´´´´´¶¶¶¶¶´´´´´¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶´´´´´¶¶¶¶¶´´´´´¶¶¶´´´´"
    echo -e "\t´´´´´´¶¶´´´¶¶¶´´´´´´´´´´´¶¶¶¶¶¶¶¶¶´´´´´´´´´´´¶¶¶´´´¶¶´´´´´´"
    echo -e "\t´´´´´´¶¶´´¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶´´¶¶´´´´´´"
    echo -e "\t´´´´´´´¶¶¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶¶¶´´´´´´´"
    echo -e "\\e${c0}"
    echo -e "\\e${c1}☠               \\e${c5}OS: \\e${c1}${OS}☠"
    echo -e "\\e${c1}☠         \\e${c5}Hostname: \\e${c1}${HOST}☠"
    echo -e "\\e${c1}☠             \\e${c5}User: \\e${c1}${USER}☠"
    echo -e "\\e${c1}☠           \\e${c5}Uptime: \\e${c1}${UPTIME}☠"
    echo -e "\\e${c1}☠           \\e${c5}Kernel: \\e${c1}${KERNEL}☠"
    echo -e "\\e${c1}☠            \\e${c5}Shell: \\e${c1}${SHELL}☠"
    echo -e "\\e${c1}☠              \\e${c5}CPU: \\e${c1}${CPU}☠"
    echo -e "\\e${c1}☠              \\e${c5}RAM: \\e${c3}${MEM_DISPLAY}"
    echo -e "\\e${c1}☠             \\e${c5}Root: \\e${c1}${ROOT_DISPLAY}☠"
    echo ""
    echo -e "\\e${c0}"
    echo -e "\\e${c4}> \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}

display_dolphin(){
    echo -e "\\e${c0}\n"
    echo -e "\t\\e${c0}____________\\e${c6}¶¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}________\\e${c6}¶¶¶¶¶________¶¶¶¶¶¶"
    echo -e "\t\\e${c0}_____\\e${c6}¶¶¶¶_________________¶¶¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}____\\e${c6}¶¶_______________________¶¶¶__¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}___\\e${c6}¶¶___________________________¶¶_¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}___\\e${c6}¶¶_____¶¶¶¶____________________¶_______¶¶"
    echo -e "\t\\e${c0}___\\e${c6}¶¶_____¶0_¶_____________________¶¶_¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}_\\e${c6}¶¶_____¶________¶¶¶¶_______________¶¶_¶¶"
    echo -e "\t\\e${c6}¶¶_____¶___¶¶¶¶¶¶¶¶¶¶¶________¶______¶_¶¶"
    echo -e "\t\\e${c6}¶¶__¶¶¶¶¶¶¶¶¶¶_____¶¶_¶_____¶__¶¶_____¶_¶¶"
    echo -e "\t\\e${c0}_\\e${c6}¶¶¶¶¶¶¶______¶_¶¶__¶_¶_____¶¶¶__¶_______¶"
    echo -e "\t\\e${c0}______________\\e${c6}¶_¶¶¶¶¶_¶_____¶¶¶¶__¶¶_____¶¶"
    echo -e "\t\\e${c0}______________\\e${c6}¶_¶¶¶¶¶¶_¶____¶__¶¶¶¶¶¶_____¶"
    echo -e "\t\\e${c0}______________\\e${c6}¶¶¶¶¶__¶_¶____¶____¶¶¶¶¶____¶¶"
    echo -e "\t\\e${c0}_______________\\e${c6}¶¶¶___¶¶_¶___¶¶¶¶__¶¶¶¶¶___¶¶"
    echo -e "\t\\e${c0}______________________\\e${c6}¶__¶__¶¶_¶¶¶__¶¶¶¶___¶"
    echo -e "\t\\e${c0}_______________________\\e${c6}¶¶¶¶__¶___¶¶__¶¶¶___¶"
    echo -e "\t\\e${c0}_________________________\\e${c6}¶¶¶¶¶_____¶_¶¶¶¶__¶¶"
    echo -e "\t\\e${c0}____________________________________\\e${c6}¶_¶¶¶__¶¶"
    echo -e "\t\\e${c0}_____________________________________\\e${c6}¶¶¶¶¶_¶¶"
    echo -e "\t\\e${c0}______________________________________\\e${c6}¶¶¶¶_¶¶"
    echo -e "\t\\e${c0}______________________________________\\e${c6}¶¶¶¶_¶¶"
    echo -e "\t\\e${c0}_______________________________________\\e${c6}¶_¶_¶"
    echo -e "\t\\e${c0}_______________________________________\\e${c6}¶___¶"
    echo -e "\t\\e${c0}_______________________________________\\e${c6}¶¶_¶¶"
    echo -e "\t\\e${c0}___________________________________\\e${c6}¶¶¶¶¶¶_¶¶¶¶"
    echo -e "\t\\e${c0}__________________________________\\e${c6}¶¶________¶¶¶¶"
    echo -e "\t\\e${c0}_________________________________\\e${c6}¶¶___________¶¶¶"
    echo -e "\t\\e${c0}_________________________________\\e${c6}¶¶_¶_¶¶¶_______¶¶"
    echo -e "\t\\e${c0}__________________________________\\e${c6}¶¶_¶¶_¶¶¶¶____¶¶"
    echo -e "\t\\e${c0}____________________________________________\\e${c6}¶¶___¶"
    echo -e "\t\\e${c0}_____________________________________________\\e${c6}¶__¶"
    echo -e "\t\\e${c0}_______________________________________________\\e${c6}¶¶\\e${c0}_"
    echo -e "\\e${c0}"
    echo -e "\\e${c6}❥               \\e${c2}OS: \\e${c6}${OS}❤"
    echo -e "\\e${c6}❥         \\e${c2}Hostname: \\e${c6}${HOST}"
    echo -e "\\e${c6}❥             \\e${c2}User: \\e${c6}${USER}"
    echo -e "\\e${c6}❥           \\e${c2}Uptime: \\e${c6}${UPTIME}"
    echo -e "\\e${c6}❥           \\e${c2}Kernel: \\e${c6}${KERNEL}"
    echo -e "\\e${c6}❥            \\e${c2}Shell: \\e${c6}${SHELL}"
    echo -e "\\e${c6}❥              \\e${c2}CPU: \\e${c6}${CPU}"
    echo -e "\\e${c6}❥              \\e${c2}RAM: \\e${c3}${MEM_DISPLAY}"
    echo -e "\\e${c6}❥             \\e${c2}Root: \\e${c6}${ROOT_DISPLAY}"
    echo ""
    echo -e "\\e${c0}"
    echo -e "\\e${c6}❥ \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}

display_snake_sword(){
    echo -e "\t\\e${c0}_______________________\\e${c1}¶¶¶¶"
    echo -e "\t\\e${c0}_______________\\e${c1}¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶_¶¶¶"
    echo -e "\t\\e${c0}_________\\e${c1}¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}_______\\e${c1}¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______\\e${c1}¶¶¶¶¶¶¶¶\\e${c0}_______\\e${c1}¶¶¶¶¶¶¶¶¶\\e${c0}___\\e${c1}¶¶¶¶"
    echo -e "\t\\e${c0}_____\\e${c1}¶¶¶¶¶¶¶______________________\\e${c1}¶¶"
    echo -e "\t\\e${c0}_____\\e${c1}¶¶¶¶¶¶___\\e${c0}¶¶¶¶¶________________\\e${c1}¶"
    echo -e "\t\\e${c0}____\\e${c1}¶¶¶¶¶¶___\\e${c0}¶¶¶1¶¶¶"
    echo -e "\t\\e${c0}____\\e${c1}¶¶¶¶¶¶___\\e${c0}¶¶111¶¶"
    echo -e "\t\\e${c0}____\\e${c1}¶¶¶¶¶¶___\\e${c0}¶¶¶1¶¶¶"
    echo -e "\t\\e${c0}____\\e${c1}¶¶¶¶¶¶____\\e${c0}¶¶1¶¶"
    echo -e "\t\\e${c0}_____\\e${c1}¶¶¶¶¶¶___\\e${c0}¶¶1¶¶"
    echo -e "\t\\e${c0}_____\\e${c1}¶¶¶¶¶¶¶¶_\\e${c0}¶¶¶¶¶"
    echo -e "\t\\e${c0}______\\e${c1}¶¶¶¶¶¶¶¶\\e${c0}¶¶¶¶¶"
    echo -e "\t\\e${c0}_______\\e${c1}¶¶¶¶¶¶¶¶¶\\e${c0}¶¶¶¶"
    echo -e "\t\\e${c0}_________\\e${c1}¶¶¶¶¶¶¶¶¶\\e${c0}¶¶¶"
    echo -e "\t\\e${c0}______¶¶¶¶\\e${c1}¶¶¶¶¶¶¶¶¶¶¶\\e${c0}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}__¶¶¶¶¶¶¶¶¶¶\\e${c1}¶¶¶¶¶¶¶¶¶¶¶¶\\e${c0}¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}____¶¶¶¶11111\\e${c1}111111111111\\e${c0}¶¶¶¶¶"
    echo -e "\t\\e${c0}_______¶¶¶¶¶¶¶¶¶¶¶¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶__\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶___\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶___\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶___\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶___\\e${c1}¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶__\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶¶¶¶¶¶\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶\\e${c1}¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}_____________\\e${c1}¶¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}____________\\e${c1}¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶¶¶¶¶\\e${c0}_¶¶"
    echo -e "\t\\e${c0}__________\\e${c1}¶¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}__________\\e${c1}¶¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}__________\\e${c1}¶¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}__________\\e${c1}¶¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}__________\\e${c1}¶¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}____________\\e${c1}¶¶\\e${c0}¶¶_1_¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶¶_\\e${c1}¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶_1_¶¶__\\e${c1}¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶\\e${c1}¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶\\e${c1}¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}_____________\\e${c1}¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}____________\\e${c1}¶¶¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶¶¶\\e${c0}___¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶¶\\e${c0}¶___¶¶"
    echo -e "\t\\e${c0}___________\\e${c1}¶¶¶\\e${c0}¶¶___¶¶"
    echo -e "\t\\e${c0}____________\\e${c1}¶¶\\e${c0}¶¶___¶¶"
    echo -e "\t\\e${c0}____________\\e${c1}¶¶\\e${c0}¶¶___¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶\\e${c1}¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶\\e${c1}¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶_\\e${c1}¶¶¶¶¶"
    echo -e "\t\\e${c0}______________¶¶___¶¶___\\e${c1}¶¶¶¶"
    echo -e "\t\\e${c0}_______________¶¶_¶¶_____\\e${c1}¶¶¶"
    echo -e "\t\\e${c0}________________¶¶¶______\\e${c1}¶¶¶"
    echo -e "\t\\e${c0}"
    echo -e "\\e${c6}☯               \\e${c7}OS: \\e${c6}${OS}"
    echo -e "\\e${c6}☯         \\e${c7}Hostname: \\e${c6}${HOST}"
    echo -e "\\e${c6}☯             \\e${c7}User: \\e${c6}${USER}"
    echo -e "\\e${c6}☯           \\e${c7}Uptime: \\e${c6}${UPTIME}"
    echo -e "\\e${c6}☯           \\e${c7}Kernel: \\e${c6}${KERNEL}"
    echo -e "\\e${c6}☯            \\e${c7}Shell: \\e${c6}${SHELL}"
    echo -e "\\e${c6}☯              \\e${c7}CPU: \\e${c6}${CPU}"
    echo -e "\\e${c6}☯              \\e${c7}RAM: \\e${c3}${MEM_DISPLAY}"
    echo -e "\\e${c6}☯             \\e${c7}Root: \\e${c6}${ROOT_DISPLAY}"
    echo ""
    echo -e "\\e${c0}"
    echo -e "\\e${c6}☯ \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}

display_broken(){
    echo -e "\t\\e${c0}_____________________________________\\e${c1}¶¶\\e${c0}___________"
    echo -e "\t\\e${c0}________________________________\\e${c1}¶1¶1111111¶\\e${c0}_______"
    echo -e "\t\\e${c0}________\\e${c1}¶¶111¶\\e${c0}_______________\\e${c1}¶¶¶¶111111111¶¶¶1\\e${c0}____"
    echo -e "\t\\e${c0}_____\\e${c1}¶1¶¶¶¶¶111111¶\\e${c0}_________\\e${c1}¶¶¶1¶¶¶11111111¶1¶¶\\e${c0}___"
    echo -e "\t\\e${c0}___\\e${c1}¶¶¶1¶1111111111¶¶1\\e${c0}______\\e${c1}¶¶1¶¶¶1111111111111¶¶¶\\e${c0}_"
    echo -e "\t\\e${c0}__\\e${c1}¶¶1¶¶1111111111111¶¶\\e${c0}_____\\e${c1}¶¶¶1¶¶¶¶1111111111111¶\\e${c0}_"
    echo -e "\t\\e${c0}__\\e${c1}¶¶_¶1111111111111111¶¶\\e${c0}___\\e${c1}¶¶¶¶¶¶11¶111111111111¶\\e${c0}_"
    echo -e "\t\\e${c0}_\\e${c1}11_¶11111111111111111¶¶\\e${c0}_____\\e${c1}¶¶¶¶\\e${c0}__\\e${c1}¶111111111111¶¶"
    echo -e "\t\\e${c1}¶¶¶¶1111111111111111¶¶¶¶\\e${c0}_____\\e${c1}1¶¶__11111111111111¶¶"
    echo -e "\t\\e${c1}¶¶¶¶11111111111¶¶¶¶¶¶¶\\e${c0}______\\e${c1}1¶1¶¶11111111111111¶1\\e${c0}_"
    echo -e "\t\\e${c1}¶¶1¶1111111111111¶¶¶¶¶¶\\e${c0}_____\\e${c1}¶¶¶¶¶¶1111111111111¶¶\\e${c0}_"
    echo -e "\t\\e${c1}¶¶11111111111111111111111¶¶\\e${c0}___\\e${c1}¶¶¶¶¶¶1111111111¶¶¶\\e${c0}_"
    echo -e "\t\\e${c0}_\\e${c1}1¶111111111111111111¶¶¶¶¶¶\\e${c0}____\\e${c1}¶¶¶¶11111111111¶1\\e${c0}__"
    echo -e "\t\\e${c0}__\\e${c1}¶¶11111111111111111¶¶¶\\e${c0}_____\\e${c1}¶¶¶1111111111111¶1\\e${c0}___"
    echo -e "\t\\e${c0}___\\e${c1}¶¶¶111111111111¶1¶¶¶\\e${c0}____\\e${c1}1¶¶111¶1111111¶11¶1\\e${c0}____"
    echo -e "\t\\e${c0}____\\e${c1}1¶¶¶11111111111¶¶¶¶111¶¶¶¶111111111¶11¶¶¶\\e${c0}_____"
    echo -e "\t\\e${c0}______\\e${c1}¶¶¶¶1111111111111¶¶¶¶1¶¶¶¶¶¶¶¶11¶11¶¶\\e${c0}_______"
    echo -e "\t\\e${c0}_______\\e${c1}¶¶¶¶¶11111111111¶111¶\\e${c0}___\\e${c1}¶¶¶111¶1¶¶¶\\e${c0}________"
    echo -e "\t\\e${c0}_________\\e${c1}¶¶¶¶¶¶111111111111¶\\e${c0}__\\e${c1}¶¶¶111¶¶¶1\\e${c0}__________"
    echo -e "\t\\e${c0}____________\\e${c1}1¶¶¶¶¶11111111¶¶\\e${c0}_\\e${c1}¶¶¶¶111¶¶\\e${c0}____________"
    echo -e "\t\\e${c0}______________\\e${c1}¶¶¶¶¶¶¶1111111\\e${c0}_\\e${c1}¶¶¶11¶¶1\\e${c0}_____________"
    echo -e "\t\\e${c0}_________________\\e${c1}1¶¶¶¶¶¶1111¶¶¶1¶¶¶¶\\e${c0}______________"
    echo -e "\t\\e${c0}____________________\\e${c1}¶¶¶¶¶¶1¶¶¶¶¶1¶\\e${c0}________________"
    echo -e "\t\\e${c0}_______________________\\e${c1}¶1¶¶¶1¶¶¶\\e${c0}__________________"
    echo -e "\t\\e${c0}___________________________\\e${c1}11¶\\e${c0}____________________"
    echo -e "\\e${c0}"
    echo -e "\\e${c6}❥               \\e${c1}OS: \\e${c6}${OS}❤"
    echo -e "\\e${c6}❥         \\e${c1}Hostname: \\e${c6}${HOST}❤"
    echo -e "\\e${c6}❥             \\e${c1}User: \\e${c6}${USER}❤"
    echo -e "\\e${c6}❥           \\e${c1}Uptime: \\e${c6}${UPTIME}❤"
    echo -e "\\e${c6}❥           \\e${c1}Kernel: \\e${c6}${KERNEL}❤"
    echo -e "\\e${c6}❥            \\e${c1}Shell: \\e${c6}${SHELL}❤"
    echo -e "\\e${c6}❥              \\e${c1}CPU: \\e${c6}${CPU}❤"
    echo -e "\\e${c6}❥              \\e${c1}RAM: \\e${c3}${MEM_DISPLAY}"
    echo -e "\\e${c6}❥             \\e${c1}Root: \\e${c6}${ROOT_DISPLAY}❤"
    echo ""
    echo -e "\\e${c0}"
    echo -e "\\e${c6}❤ \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}

display_cute_bird(){
    echo -e "\t\\e${c0}´´´´´´´´´´´´´´´´´\\e${c3}¶"
    echo -e "\t\\e${c0}´´´´´´´´´´´´´´\\e${c3}¶´´¶´´´¶¶"
    echo -e "\t\\e${c0}´´´´´´´´´´´´´´\\e${c3}¶´¶¶´¶¶"
    echo -e "\t\\e${c0}´´´´´´´´´\\e${c3}¶¶¶¶´´´´´´¶¶¶¶¶¶"
    echo -e "\t\\e${c0}´´´´´´´\\e${c3}¶¶´´´´´´´´´´´´´´´´¶¶"
    echo -e "\t\\e${c0}´´´´´\\e${c3}¶¶´´´´´´´´¶¶´´´´´´´´´´¶¶"
    echo -e "\t\\e${c0}´´\\e${c3}´¶¶´´´´´´´´´´´´´´´´´´´´´´´´¶¶\t\\e${c6}            \\e${c1} OS: \\e${c3}$OS"
    echo -e "\t\\e${c0}´´\\e${c3}¶¶´´´´´´´´´´´´´´´´´´´´´´´´´´¶¶\t\\e${c6}\\e${c1}Hostname: \\e${c3}$HOST"
    echo -e "\t\\e${c0}´´\\e${c3}¶´´´´´´´´´´´´´´´´´´´´´´´´´´´¶´¶\t\\e${c6}   \\e${c1} User: \\e${c3}$USER"
    echo -e "\t\\e${c0}´\\e${c3}¶´´´´´´´´´´´´´´´´¶´´´´´´´´´´´´´¶\t\\e${c6}   \\e${c1} User: \\e${c3}$USER"
    echo -e "\t\\e${c0}´\\e${c3}¶´´´´´´´´´´´´´¶¶¶¶´´´´´´´´´´´´´´¶\t\\e${c6} \\e${c1} Uptime: \\e${c3}$UPTIME"
    echo -e "\t\\e${c0}´\\e${c3}¶´´´´´´´´´´´´¶¶´¶´´´´´´´´´´´¶´´´¶\t\\e${c6} \\e${c1} Kernel: \\e${c3}$KERNEL"
    echo -e "\t\\e${c0}´\\e${c3}¶´´´´´´´´´´¶¶¶¶¶¶´´´´´´´¶¶¶¶´´´´¶\t\\e${c6}  \\e${c1} Shell: \\e${c3}$SHELL"
    echo -e "\t\\e${c0}´\\e${c3}¶´´´´´´´´´¶¶¶¶¶¶¶´´´´´´¶¶´´¶´´´´¶\t\\e${c6}    \\e${c1} CPU: \\e${c3}$CPU"
    echo -e "\t\\e${c0}´´\\e${c3}¶´´´´´´´´¶¶¶¶¶´¶´´´´´¶¶¶¶¶¶´´´¶\t\\e${c6}    \\e${c1} RAM: \\e${c6}${MEM_DISPLAY}"
    echo -e "\t\\e${c0}´´\\e${c3}¶¶´´´´´´´¶´´´´´¶´´´´¶¶¶¶¶¶´´´¶¶\t\\e${c6}   \\e${c1} Root: \\e${c3}${ROOT_DISPLAY}"
    echo -e "\t\\e${c0}´´´\\e${c3}¶¶´´´´´´¶´´´´¶´´´´¶¶¶¶´´´´´¶"
    echo -e "\t\\e${c0}´´´´\\e${c3}¶´´´´´´¶´´´¶´´´´´¶´´´´´´´¶"
    echo -e "\t\\e${c0}´´´´\\e${c3}¶´´´´´´¶¶¶¶´´´´´´´´´¶´´¶¶"
    echo -e "\t\\e${c0}´´´´\\e${c3}¶¶´´´´´´´´´´´´´´´¶¶¶´´¶"
    echo -e "\t\\e${c0}´´´´´\\e${c3}¶¶¶´´´´´´´¶¶¶¶¶´´´´´´¶"
    echo -e "\t\\e${c0}´´´´´´´´\\e${c3}¶¶¶´´´´´¶¶´´´´´´´¶¶"
    echo -e "\t\\e${c0}´´´´´´´´´´´´\\e${c3}¶¶´´´´´¶¶¶¶¶¶´"
    echo -e "\t\\e${c0}´´´´´´´´´´\\e${c3}¶¶´´´´´´¶¶´¶"
    echo -e "\t\\e${c0}´´´´´´´\\e${c3}¶¶¶¶´´´´´´´´¶´¶¶"
    echo -e "\t\\e${c0}´´´´´´´´´\\e${c3}¶´´¶¶´´´´´¶´´´¶"
    echo -e "\t\\e${c0}´´´´\\e${c3}¶¶¶¶¶¶´¶´´´´´´´¶´´¶´"
    echo -e "\t\\e${c0}´´\\e${c3}¶¶´´´¶¶¶¶´¶´´´´´´¶´´´¶¶¶¶¶¶¶"
    echo -e "\t\\e${c0}´´\\e${c3}¶¶´´´´´´¶¶¶¶´´´´´¶´¶¶´´´´´¶¶"
    echo -e "\t\\e${c0}´´\\e${c3}¶´´´´´´´´´´¶¶¶¶¶¶¶¶´´´´´´´´´¶"
    echo -e "\t\\e${c0}´´´\\e${c3}¶¶´´´´´´´´´¶\\e${c0}´´´\\e${c3}¶´´´´´´´´´´¶"
    echo -e "\t\\e${c0}´´´´\\e${c3}¶¶¶¶¶¶¶¶¶¶¶\\e${c0}´´´\\e${c3}¶¶¶¶¶¶¶¶¶¶¶\\e${c0} ~*"
    echo -e "\t\\e${c0}"
    echo -e "\\e${c2}            ⊕ ☎ ☏  ❥ \\e${c6}${QUOTE_DISPLAY}\\e${c0}\n"
}

display_arch(){
    echo -e "\\e${c0}"
    echo -e "\t\\e${c4}                   -\`"
    echo -e "\t\\e${c4}                  .o+\`"
    echo -e "\t\\e${c4}                 \`ooo/"
    echo -e "\t\\e${c4}                \`+oooo:"
    echo -e "\t\\e${c4}               \`+oooooo:\t\\e${c6}         \\e${c1} OS: \\e${c4}$OS"
    echo -e "\t\\e${c4}               -+oooooo+:\t\\e${c6}    \\e${c1}Hostname: \\e${c4}$HOST"
    echo -e "\t\\e${c4}             \`/:-:++oooo+:\t\\e${c6}       \\e${c1} User: \\e${c4}$USER"
    echo -e "\t\\e${c4}            \`/++++/+++++++:\t\\e${c6}     \\e${c1} Uptime: \\e${c4}$UPTIME"
    echo -e "\t\\e${c4}           \`/++++++++++++++:\t\\e${c6}     \\e${c1} Kernel: \\e${c4}$KERNEL"
    echo -e "\t\\e${c4}          \`/+++ooooooooooooo/\`\t\\e${c6}      \\e${c1} Shell: \\e${c4}$SHELL"
    echo -e "\t\\e${c4}         ./ooosssso++osssssso+\`\t\\e${c6}        \\e${c1} CPU: \\e${c4}$CPU"
    echo -e "\t\\e${c4}        .oossssso-\`\`\`\`/ossssss+\`\t\\e${c6}\\e${c1} RAM: \\e${c6}${MEM_DISPLAY}"
    echo -e "\t\\e${c4}       -osssssso.      :ssssssso.\t\\e${c6}\\e${c1}Root: \\e${c4}${ROOT_DISPLAY}"
    echo -e "\t\\e${c4}      :osssssss/        osssso+++."
    echo -e "\t\\e${c4}     /ossssssss/        +ssssooo/-"
    echo -e "\t\\e${c4}   \`/ossssso+/:-        -:/+osssso+-"
    echo -e "\t\\e${c4}  \`+sso+:-\`                 \`.-/+oso:"
    echo -e "\t\\e${c4}\`++:.                           \`-/+/"
    echo -e "\t\\e${c4}.\`                                 \`/"
    echo -e "\\e${c0}"
    echo -e "✰ \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}
display_gentoo(){
    echo -e "\\e${c2}                                           ."
    echo "     .siv.                                d\@b"
    echo "  .d@@@@@@b.    .cd@@b.     .d@@b.   d@@@@@@@@@@@b  .d@@b.      .d@@b."
    echo "  @@@@( )@@@b d@@( )@@@.   d@@@@@@@b Q@@@@@@@P@@@P.@@@@@@@b.  .@@@@@@@b."
    echo "  Q@@@@@@@@@@B@@@@@@@@P\"  d@@@PQ@@@@b.   @@@@.   .BOOB' \`@@@ .@@@P' \`@@@"
    echo "    \"@@@@@@@P Q@@@@@@@b  d@@@P   Q@@@@b  @@@@b   @@@@b..d@@@ @@@@b..d@@@"
    echo "   d@@@@@@P\"   \"@@@@@@@@ Q@@@     Q@@@@  @@@@@   \`Q@@@@@@@P  \`Q@@@@@@@P"
    echo "  @@@@@@@P       \`\"\"\"\"\"   \"\"        \"\"   Q@@@P     \"Q@@@P\"     \"Q@@@P\""
    echo "  \`Q@@P\"                                  \"\"\""
    echo -e "\\e${c0}"
    echo -e "\\e${c4}♠               \\e${c5}OS: \\e${c4}${OS}"
    echo -e "\\e${c4}♠         \\e${c5}Hostname: \\e${c4}${HOST}"
    echo -e "\\e${c4}♠             \\e${c5}User: \\e${c4}${USER}"
    echo -e "\\e${c4}♠           \\e${c5}Uptime: \\e${c4}${UPTIME}"
    echo -e "\\e${c4}♠           \\e${c5}Kernel: \\e${c4}${KERNEL}"
    echo -e "\\e${c4}♠            \\e${c5}Shell: \\e${c4}${SHELL}"
    echo -e "\\e${c4}♠              \\e${c5}CPU: \\e${c4}${CPU}"
    echo -e "\\e${c4}♠              \\e${c5}RAM: \\e${c3}${MEM_DISPLAY}"
    echo -e "\\e${c4}♠             \\e${c5}Root: \\e${c4}${ROOT_DISPLAY}"
    echo ""
    echo -e "\\e${c0}"
    echo -e "\\e${c4}♠ \\e${c3}${QUOTE_DISPLAY}\\e${c0}\n"
}
# **** get it ****
arg=$1
case $arg in
    -x){
	    declaration
            OS='Danger Gnu/Linux'
	    lame_quote_gentoo
	    display_danger
	};;
    -g){
	    declaration
            OS='Gentoo Gnu/Linux'
            lame_quote_gentoo
            display_gentoo
	};;
    -d){
	    declaration
            lame_quote_dolphin
            display_dolphin
	};;
    -r){
	    declaration
            lame_quote_broken
            display_broken
	};;
    -s){
	    declaration
            lame_quote_snake_sword
            display_snake_sword
	};;
    -b){
	    declaration
            lame_quote_cute_bird
            display_cute_bird
	};;
    -a){
            declaration
	    OS='Arch Gnu/linux'
            lame_quote_arch
            display_arch
        };;
    -h){
	    echo -e "XSS : X System Show\n"
	    echo "Usage: /path/to/xss [argument]"
	    echo "List of arguments,"
	    echo -e "\t-x >\tDanger Linux Theme"
	    echo -e "\t-d >\tDolphin Theme"
	    echo -e "\t-r >\tBroken Theme"
	    echo -e "\t-s >\tSnake Sword Theme"
	    echo -e "\t-b >\tCute Bird Theme"
	    echo -e "\t-g >\tGentoo Linux Theme"
	    echo -e "\t-a >\tArch Linux Theme"
	    echo -e "\t-h >\tShow Help"
	    echo "Example: /path/to/siv -x"
	};;
    *){
	    echo -e "XSS : X System Show\n"
	    echo "Usage: /path/to/xss [argument]"
	    echo "List of arguments,"
	    echo -e "\t-x >\tDanger Linux Theme"
	    echo -e "\t-d >\tDolphin Theme"
	    echo -e "\t-r >\tBroken Theme"
	    echo -e "\t-s >\tSnake Sword Theme"
	    echo -e "\t-b >\tCute Bird Theme"
	    echo -e "\t-g >\tGentoo Linux Theme"
	    echo -e "\t-a >\tArch Linux Theme"
	    echo -e "\t-h >\tShow Help"
	    echo "Example: /path/to/siv -x"
	};;
esac
# EOF
