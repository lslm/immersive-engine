CC = clang
CXX = clang++ -std=c++17
CFLAGS = -Wno-deprecated-declarations
LDFLAGS = lib/glfw/src/libglfw3.a lib/glad/src/glad.o lib/spdlog/libspdlog.a
LDFLAGS += -Ilib/spdlog/include -Ilib/glfw/include -Ilib/glad/include -Isrc
LDFLAGS += -framework OpenGL -framework IOKit -framework CoreVideo -framework Cocoa

SRC = $(wildcard src/**/*.cpp src/**/**/*.cpp)
OBJ = $(SRC:.c=.o)
BIN = bin

all: dirs libs game

libs:
	cd lib/spdlog && cmake . && make
	cd lib/glad && $(CC) -o src/glad.o -Iinclude -c src/glad.c
	cd lib/glfw && cmake . && make

dirs:
	mkdir -p ./$(BIN)

game: $(OBJ)
	$(CXX) $(CFLAGS) -dynamiclib -o $(BIN)/libengine.dylib $^ $(LDFLAGS)

%.o: %.cpp
	$(CXX) -o $@ -c $<

clean:
	rm -rf $(BIN) $(OBJ)
