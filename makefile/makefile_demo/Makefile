Obj = main.o hello.o

main: $(Obj) 
	g++ -o main $(Obj)

main.o: hello.h

hello.o: hello.h

.PHONY: clean

clean:
	rm main $(Obj)
