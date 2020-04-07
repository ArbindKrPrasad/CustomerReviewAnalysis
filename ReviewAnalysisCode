import csv
from textblob import TextBlob
import nltk
from newspaper import Article
import urllib.parse

sent_code = 0.0


#Searching the product
with open('amazonreview44.csv') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=',')

    product_input = input("Enter the name of the product you want to search: ")
    searched_pid = "null"
    for row in csv_reader:
        if product_input in row[6]:
            print("Product found:\t {}".format(row[6]))
            searched_pid = row[0]
            break

    if searched_pid == "null":
        print("Item Not Found! Please Enter the correct Keyword! ")
        exit()

max_pos_rev = "null"
min_pos_rev = "null"

max_pos_rev_num = -1
min_pos_rev_num = 1

top_pos_username = "null"
top_neg_username = "null"

overall_rating = 0

with open('amazonreview44.csv') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=',')
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            line_count += 1
            continue
        else:
            if(row[0]==searched_pid):
                #lst.append(row[2])


                #Get the article
                article = row[3]

                #Create a text blob object
                obj = TextBlob(article)
                overall_rating+=int(row[2])
                sentiment = obj.sentiment.polarity


                if sentiment>max_pos_rev_num:
                    max_pos_rev_num = sentiment
                    max_pos_rev = row[3]
                    top_pos_username = row[5]
                if sentiment<min_pos_rev_num:
                    min_pos_rev_num = sentiment
                    min_pos_rev = row[3]
                    top_neg_username = row[5]

                sent_code +=sentiment
                line_count += 1


print(max_pos_rev_num)
print(min_pos_rev_num)
print("\n\nTop Positive review with a sentiment of: {:.2f} \n\t{} \t by {}".format(max_pos_rev_num,max_pos_rev,top_pos_username))
print("\n\nTop Negative review with a sentiment of: {:.2f} \n\t{} \t by {}".format(m,min_pos_rev,top_neg_username))

print(f'\n\nTotal Number of reviews analysed:  {line_count} ')
overall_analysis=sent_code/line_count
print("\n\nFinal Sentiment: (Scale: -1 means worst and 1 means best): \t{:.2f}\n\n".format(overall_analysis))



if overall_analysis>0.4:
    print("The product is excellent and don't hazitate to buy the product!")
elif overall_analysis>0.3:
    print("The product is good and it is recommended to buy!")
elif overall_analysis>0.2:
    print("The product is Okey and you can buy it!")
elif overall_analysis>0.1:
    print("The product is somehow manageable but you can look around for other similar products")
elif overall_analysis>0.0:
    print("The product is neutral and it can be good or bad piece depending on your luck!")
elif overall_analysis>0.5:
    print("The product is not recomended at all!")
else:
    print("The product is worse, Don't buy it ever!")

print("Overall Rating of the product is {:.2f} out of 5".format(overall_rating/line_count))

