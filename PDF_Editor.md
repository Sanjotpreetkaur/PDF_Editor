#task of merging, splitting, and compressing PDFs
from PyPDF2 import PdfReader, PdfWriter
from spire.pdf import *

file_path = r'sample_file'
file_name = "resulting_file.pdf"
file_list = [
            r"file_1"
            ,r"file_2"
            ]


def pdf_trim(file_path, file_name):
    #pdf trim
    input_pdf = PdfReader(file_path, file_name)
    output_pdf = PdfWriter()
    for page in input_pdf.pages[0:2]:
        output_pdf.add_page(page)
    output_pdf.write(file_name)

def spire_pdf_compression(file_path, file_name):
    #compression of PDFs
    compressor = PdfCompressor(file_path)
    compression_options = compressor.OptimizationOptions
    compression_options.SetImageQuality(ImageQuality.High)
    compression_options.SetResizeImages(True)
    compression_options.SetIsCompressImage(True)
    compressor.CompressToFile(file_name)
    
def merge_pdf(files, file_name):
    #merging of PDFs
    writer = PdfWriter()
    for i in files:
        reader = PdfReader(i)
        for page in reader.pages:
            writer.add_page(page)
    writer.write(file_name)
