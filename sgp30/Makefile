sensirion_common_dir := ../embedded-common
sgp_common_dir := ../sgp-common
sw_i2c_dir := ${sensirion_common_dir}/sw_i2c
hw_i2c_dir := ${sensirion_common_dir}/hw_i2c

CFLAGS := -Os -Wall -Werror -I. -I${sensirion_common_dir} -I${sgp_common_dir}

sensirion_common_objects := sensirion_common.o
sgp30_binaries := sgp30_example_usage_hw_i2c sgp30_example_usage_sw_i2c
sgp30_featureset := sgp30_featureset.o
sgp_featuresets += ${sgp30_featureset}
sgp_binaries += ${sgp30_binaries}

sw_objects := sensirion_sw_i2c.o sensirion_sw_i2c_implementation.o
hw_objects := sensirion_hw_i2c_implementation.o
all_objects := ${sensirion_common_objects} ${hw_objects} ${sw_objects} ${sgp_featuresets} sgp30.o

.PHONY: all

all: ${sgp_binaries}

sensirion_common.o:
	$(CC) $(CFLAGS) -c -o $@ $^ ${sensirion_common_dir}/sensirion_common.c
sensirion_sw_i2c_implementation.o:
	$(CC) $(CFLAGS) -c -o $@ $^ ${sw_i2c_dir}/sensirion_sw_i2c_implementation.c
sensirion_hw_i2c_implementation.o:
	$(CC) $(CFLAGS) -c -o $@ $^ ${hw_i2c_dir}/sensirion_hw_i2c_implementation.c

sensirion_sw_i2c.o:
	$(CC) -I${sw_i2c_dir} $(CFLAGS) -c -o $@ $^ ${sw_i2c_dir}/sensirion_sw_i2c.c

sgp30.o: ${sgp_common_dir}/sgp_featureset.h ${sensirion_common_dir}/sensirion_i2c.h sgp30.c sgp30.h

sgp30_example_usage_sw_i2c: ${sensirion_common_objects} ${sw_objects} ${sgp_featuresets} sgp30.o
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^ $(LOADLIBES) $(LDLIBS) sgp30_example_usage.c

sgp30_example_usage_hw_i2c: ${sensirion_common_objects} ${hw_objects} ${sgp_featuresets} sgp30.o
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^ $(LOADLIBES) $(LDLIBS) sgp30_example_usage.c

clean:
	$(RM) ${all_objects} ${sgp_binaries}