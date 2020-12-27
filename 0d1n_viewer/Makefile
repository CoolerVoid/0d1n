CC=gcc
CFLAGS=-Wall -Wextra -Wno-unknown-pragmas -O2
DFLAGS=-DMG_ENABLE_SSL -DMG_DISABLE_PFS lib/libmongoose/mongoose.c lib/BSD/strsec.c lib/frozen/frozen.c
HARDENING= -fstack-protector-all -pie -fPIE
DIR=src/
DIROUT=bin/
UNAME_S := $(shell uname -s)
#ifeq ($(UNAME_S),Darwin)
LDFLAGS=-lpthread -lcrypto -lssl -lm
#else
#	LDFLAGS=-Wl,-z,relro,-z,now -lpthread -lm -lcrypto -lssl
#endif

0d1n_view: $(DIR)0d1n_view.c
	@echo "Compile... "
	$(CC) $(CFLAGS) $(DFLAGS) -c $(DIR)*.c
	$(CC) -o $(DIROUT)0d1n_view *.o $(LDFLAGS) $(HARDENING)
	rm *.o
	@echo "end  "
	@echo " Next step, execute \"bin/0d1n_view\" to start...  "

clean:
	rm -f *.o bin/0d1n_view
install:
	make
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	install -m 0755 bin/0d1n_view $(DESTDIR)$(PREFIX)/bin
	mkdir /opt/0d1n/server/
	cp -rf cert /opt/0d1n/server/
	cp config/allowlist.txt /opt/0d1n/server/
	chmod 0755 -R /opt/0d1n/view/
	chown ${USER} -R /opt/0d1n

uninstall:
	rm $(DESTDIR)$(PREFIX)/bin/0d1n_view
	rm -rf /opt/0d1n/server
