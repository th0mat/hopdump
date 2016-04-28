#################################################################################

hopdump - tcpdump plus channel hopping

th.natter@gmail.com

#################################################################################

Works for OSX and uses the aiport utility to disassociate and change channels

hopdump is a python wrapper around tcpdump adding the following 
functionality:

- you can set the channels you want to be hopped
- you can set how long to remain on each channel
- after hopping the wifi interface is put back up  


Example usage:

# to use default hop settings and run the tcpdump command with the
# options '-i en0 -I' (interface en0, capture in monitor mode)

sudo ./hopdump --cmd="tcpdump -i en0 -I"

-------------------------------------------------------------------

# as above, plus setting the channels to be hopped

sudo ./hopdump -c 1 3 5 7 9 11 --cmd="tcpdump -i en0 -I"

-------------------------------------------------------------------

# as above, plus setting the time to remain on a channel 
# to 0.01 seconds

sudo ./hopdump -c 1 3 5 7 9 11 -r 0.01 --cmd="tcpdump -i en0 -I"

-------------------------------------------------------------------

# as above, plus setting the total hopping time to one hour
# the hopping can always be interrupted with ctrl-c

sudo ./hopdump -c 1 3 5 7 9 11 -r 0.01 -t 3600 --cmd="tcpdump -i en0 -I"



usage: sudo ./hopdump [-h] [-t TIME] [-r REMAIN] [-c [CHANNELS [CHANNELS ...]]]
                  [--cmd CMD]

optional arguments:
  -h, --help            show this help message and exit
  -t TIME, --time TIME  hopping time in sec [default = 60]
  -r REMAIN, --remain REMAIN
                        time in sec to reamin on each channel [default = 5]
  -c [CHANNELS [CHANNELS ...]], --channels [CHANNELS [CHANNELS ...]]
                        channel numbers with spaces in between [default = 1 6
                        11]
 
  --cmd CMD             command to be passed to system after hopping started
                        [example: --cmd='tcpdump -i en0 -I -w
                        dump.pcap'][default: 'not set -> try: hopdump --help']
