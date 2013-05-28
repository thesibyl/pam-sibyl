# put common definitions in here
CC	  = gcc
CFLAGS    = -Wall -fno-stack-protector # -DDEBUG -g (Ubuntu stack...)
INC       = -I./lib # will be in other dirs
INC_OSX   = -I./lib -I/opt/local/include
LIBD_OSX  = -L/opt/local/lib -L../lib
LD	  = ld
LDFLAGS   = 
LIBS      = -lpam -lcrypto
LIBDIR    = "./lib"
SIBYL     = 1
PAM_SRC   = "./pam"
# .SILENT :


default: pam_sibyl

libs:
	cd $(LIBDIR) && $(MAKE) $(MFLAGS)

pam_sibyl: libs
	$(CC) $(CFLAGS) $(INC) -fPIC -c $(PAM_SRC)/sibyl_support.c -o $(PAM_SRC)/sibyl_support.o
	$(CC) $(CFLAGS) $(INC) -fPIC -c $(PAM_SRC)/pam_sibyl.c -o $(PAM_SRC)/pam_sibyl.o
	ld -x --shared -o $(PAM_SRC)/pam_sibyl.so $(PAM_SRC)/pam_sibyl.o $(PAM_SRC)/sibyl_support.o $(LIBDIR)/bsd-base64.o $(LIBS)

debug: libs
	$(CC) $(CFLAGS) -DDEBUG -g $(INC) -fPIC -c $(PAM_SRC)/sibyl_support.c -o $(PAM_SRC)/sibyl_support.o
	$(CC) $(CFLAGS) -DDEBUG -g $(INC) -fPIC -c $(PAM_SRC)/pam_sibyl.c -o $(PAM_SRC)/pam_sibyl.o
	ld -x --shared -o $(PAM_SRC)/pam_sibyl.so $(PAM_SRC)/pam_sibyl.o $(PAM_SRC)/sibyl_support.o $(LIBDIR)/bsd-base64.o $(LIBS)

pam_sibyl-osx: libs
	$(CC) $(CFLAGS) $(INC_OSX) -fPIC -c $(PAM_SRC)/sibyl_support.c -o $(PAM_SRC)/sibyl_support.o
	$(CC) $(CFLAGS) $(INC_OSX) -fPIC -c $(PAM_SRC)/pam_sibyl.c -o $(PAM_SRC)/pam_sibyl.o
	gcc -dynamiclib -o $(PAM_SRC)/pam_sibyl.so $(PAM_SRC)/pam_sibyl.o $(PAM_SRC)/sibyl_support.o $(LIBD_OSX) $(LIBDIR)/bsd-base64.o $(LIBS)
#	ld -x -o pam_sibyl.so pam_sibyl.o sibyl_support.o $(LIBD_OSX) $(LIBDIR)/bsd-base64.o $(LIBS)

debug-osx: libs
	$(CC) $(CFLAGS) -DDEBUG -g $(INC_OSX) -fPIC -c $(PAM_SRC)/sibyl_support.c -o $(PAM_SRC)/sibyl_support.o
	$(CC) $(CFLAGS) -DDEBUG -g $(INC_OSX) -fPIC -c $(PAM_SRC)/pam_sibyl.c -o $(PAM_SRC)/pam_sibyl.o
	gcc -dynamiclib -o $(PAM_SRC)/pam_sibyl.so $(PAM_SRC)/pam_sibyl.o $(PAM_SRC)/sibyl_support.o $(LIBD_OSX) $(LIBDIR)/bsd-base64.o $(LIBS)
#	ld -x -o pam_sibyl.so pam_sibyl.o sibyl_support.o $(LIBD_OSX) $(LIBDIR)/bsd-base64.o $(LIBS)

clean:
	@find . \( -iname "*.o" -or -iname "*~" -or -iname "*.so" \) -exec rm -f '{}' \;
