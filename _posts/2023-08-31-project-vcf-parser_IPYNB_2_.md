---
title: Python VCF parser code
toc: True
description: None
courses: {'csp': {'week': 2}}
categories: ['C3.0', 'C3.1', 'C4.1']
type: tangibles
---

## VCF python parser I've been using at the lab

### Aditional comments are there to understand the code conceptually, it is a bit out of scope for the class but it's a cool project that I've been working on
- Unfortunately because the data is supposed to be confidential for my lab, I will not be sharing any of the data sets here
- Code utilizes command arguments with the arg parser
- Reads and parses genotypes and compares the total amount of differences between them
- Additionally, utilizes multiprocessing to read through multiple vcf files, thus why I will not preprocess inputs / outputs like I do with the other lab notebooks because it's just too CPU heavy. However, I will be demoing on a virtual machine.



```python
import pysam
import concurrent.futures
import argparse
import time
start_time = time.time()

def remap_genotype(gt, ref, alt):
    # Remap the genotype based on swapped alleles.
    if isinstance(gt, tuple):  # If gt is a tuple, convert to string
        gt = "/".join(str(x) for x in gt)
        
    gt_fields = gt.split("/")
    remapped_fields = []
    #Basically takes the number and then it appends the actual letter to the list called remapped_fields
    for field in gt_fields:
        if field == "0":
            remapped_fields.append(ref)
        elif field == "1":
            remapped_fields.append(alt)
        else:
            remapped_fields.append(".")

    return "/".join(remapped_fields)

def compare_genotypes(record1, record2, allele_map):
    differences = 0

    if record1.pos == record2.pos and record1.chrom == record2.chrom:
        ref1, alt1 = allele_map.get(record1.id, (record1.ref, record1.alts[0])) # Get record 1's reference and record 1's alternate alleles via their ID
        ref2, alt2 = allele_map.get(record2.id, (record2.ref, record2.alts[0])) # Same thing as above but you basically just get it for record 2 nothing too complciated, could possibly made it faster with like use of tabix or something but yeah
    

        samples1 = list(record1.samples.values())  # Get all samples in file 1
        samples2 = list(record2.samples.values())  # Get all samples in file 2

        for i in range(len(samples1)):
            sample1 = samples1[i]
            sample2 = samples2[i]

            gt1 = sample1["GT"]
            gt2 = sample2["GT"]

            # Remap genotypes if references don't match or if the alterante don't match up
            if ref1 != ref2 or alt1 != alt2:
                gt1 = remap_genotype(gt1, ref1, alt1)
                gt2 = remap_genotype(gt2, ref2, alt2)

            # Compare the remapped genotypes via the remapped genotypes list which is now represented in G1, G2
            if gt1 != gt2:
                differences += 1
                print(f"Position: {record1.chrom}:{record1.pos}")
                print(f"Sample {i}:")
                print(f"GT1: {gt1}, GT2: {gt2}")
                print(f"Ref1: {ref1}, Alt1: {alt1}")
                print(f"Ref2: {ref2}, Alt2: {alt2}")
                print("-" * 40)

    return differences

def compare_vcf_files(vcf_file1, vcf_file2, dev_mode=False): #If nothing's passed then no dev mode and it'll just pass out the thing
    differences = 0

    allele_map = {}  # A dictionary to store ref and alt alleles for each record ID
    with pysam.VariantFile(vcf_file1) as vcf1, pysam.VariantFile(vcf_file2) as vcf2:
        for record in vcf1:
            allele_map[record.id] = (record.ref, record.alts[0])  # Assuming single alternate allele

        # Use concurrent processing to compare genotypes
        with concurrent.futures.ThreadPoolExecutor() as executor:
            futures = []
            for record1 in vcf1.fetch():
                for record2 in vcf2.fetch(record1.chrom, record1.pos, record1.pos + 1):
                    future = executor.submit(compare_genotypes, record1, record2, allele_map)
                    futures.append(future)

            for future in concurrent.futures.as_completed(futures):
                differences += future.result()

    return differences



'''
Usage case:

python compare.py vcf_file_1 vcf_file_2 --dev_mode

Basically dev mode gives u a nice prints so you can see what it thinks/counts as a mutation
Right now it does not consider the indel mutations (if for example ref1 does not match up with ref2, but ref2 is longer it will still count it as a mutation for now) but that should be an easy check with the compare_genotypes for length
But for now since things have been kinda busy I'm just gonna send what I have right now, since we have to deal with indel mutations later anyway

'''
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Compare two VCF files and find genotype differences.")
    parser.add_argument("vcf_file1", type=str, help="Path to the first VCF file")
    parser.add_argument("vcf_file2", type=str, help="Path to the second VCF file")
    parser.add_argument("--dev_mode", action="store_true", help="Enable developer mode with print statements")
    args = parser.parse_args()

    differences = compare_vcf_files(args.vcf_file1, args.vcf_file2, args.dev_mode)

    # Time execution (some rando thing I copied from stack overflow to print the time):
    end_time = time.time()
    total_time = end_time - start_time
    minutes = int(total_time // 60)
    seconds = total_time % 60
    print("Number of genotype differences:", differences)
    print(f"Execution time: {minutes} minutes and {seconds:.2f} seconds")





# Before it was commandline parsed
# vcf_file1 = "/home/will/Downloads/mock_data_vcf_1/NDAR-INV119XNUX_S2_merged_L001_markdup_recalibrated_Haplotyper_MOCKDATA.vcf.gz"
# vcf_file2 = "/home/will/Downloads/mock_data_vcf_1/NDAR-INV1GBYJF8_L001_markdup_recalibrated_Haplotyper_MOCKDATA.vcf.gz"
# differences = compare_vcf_files(vcf_file1, vcf_file2)
# print("Number of genotype differences:", differences)

```
