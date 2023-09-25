cmake_minimum_required (VERSION 3.8)

project (Corth VERSION 0.0.1)

set(SOURCE_FILES 
	"src/lollipop.cpp"
)

set(HEADER_FILES "src/Errors.h")

# Add source files project.
add_executable (lollipop ${HEADER_FILES} ${SOURCE_FILES})
