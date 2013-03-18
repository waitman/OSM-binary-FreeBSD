
CXX = g++
CXXFLAGS = -O3 -I/usr/local/include
AR = ar

all: libosmpbf.a ../include/osmpbf/fileformat.pb.h ../include/osmpbf/osmformat.pb.h

libosmpbf.a: fileformat.pb.o osmformat.pb.o
	$(AR) -cr $@ fileformat.pb.o osmformat.pb.o

%.pb.o: %.pb.cc
	$(CXX) $(CXXFLAGS) -c -o $@ $<

%.pb.cc ../include/osmpbf/%.pb.h: %.proto
	protoc --proto_path=. --cpp_out=. $<
	cp *.pb.h ../include/osmpbf/

install:
	install -m 755 -g wheel -o root -d $(DESTDIR)/usr/local/lib
	install -m 644 -g wheel -o root libosmpbf.a $(DESTDIR)/usr/local/lib
	install -m 755 -g wheel -o root -d $(DESTDIR)/usr/local/include/osmpbf
	install -m 644 -g wheel -o root ../include/osmpbf/osmpbf.h $(DESTDIR)/usr/local/include/osmpbf
	install -m 644 -g wheel -o root ../include/osmpbf/fileformat.pb.h $(DESTDIR)/usr/local/include/osmpbf
	install -m 644 -g wheel -o root ../include/osmpbf/osmformat.pb.h $(DESTDIR)/usr/local/include/osmpbf

clean:
	rm -f *.pb.h *.pb.cc *.pb.o libosmpbf.a

