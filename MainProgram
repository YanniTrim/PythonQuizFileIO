def get_answer_key(quiz_id):

    myfile = open("quizzes.txt", "r")
    data = myfile.read()
    myfile.close()

    lines = data.split("\n") # splits each line into different list items

    for line in lines:
        info = line.split(",") #split Quiz ID from answers

        if info[0] == quiz_id: # if the quiz ID is the one we want
            return info[1] # return the answers for that quiz

    return "?"
        


while True:
    print("\nNYU Quizzing System - Main Menu")
    op = input("(q)uiz info, (s)core a file, or (e)exit: ")

    if op== "e":
        print("Goodbye!")
        break

    elif op == "s":

        #get the name of a class file
        filename = input("Enter a class file to score: ")

        #open this file for reading
        try:
            myfile = open(filename, "r")
            data = myfile.read().strip()
            myfile.close()
        except:
            print("Can't open file")
        else:
            lines = data.split("\n")
            quiz_name = lines[0]
            students = lines[1:] #leaves long list of all answer strings


            # get the answer key for this quiz
            key = get_answer_key(quiz_name)

            print("This file contains", len(students), "students for quiz '" + quiz_name + "'")
            print("The answer key is:", key)

            
            if len(filename) == 11:
                newfile = open(filename[0:7] + "_scored.txt", "w")
            elif len(filename) == 12:
                newfile = open(filename[0:8] + "_scored.txt", "w")

            
            scores = []
            for student in students:
                sep_student = student.split(",")
                stu_num = sep_student[0]
                stu_ans = sep_student[1]


                correct = 0
                # finding scores
                for answer in range(len(stu_ans)): 
                    if stu_ans[answer] == key[answer]:
                        correct += 1

                score = (correct/(len(stu_ans)))*100 # percentage score
                scores += [correct]
                print(f"{stu_num} earned {correct} out of {len(stu_ans)} ({format(score, '.2f')}%)")

                newfile.write(stu_num + ',' + format(score, '.2f'))
                newfile.write("\n")

            newfile.close()
            # processing scores for report
            avg_score = format(sum(scores) / len(scores), ".2f")
            max_score = max(scores)
            min_score = min(scores)
            score_range = max_score - min_score

            # find mode
            unique_scores = []
            count = []
            for i in scores:
                if i not in unique_scores:
                    unique_scores.append(i)
                    count.append(1)
                else:
                    position = unique_scores.index(i)
                    count[position]+= 1

                    
            # find mode and account for
            mode = ''
            for i in range(len(count)):
                if count[i] == max(count):
                    mode += (str(unique_scores[i]))
                    mode += ' '
                    
            print('*** Class Report ***')
            print("Average score:", avg_score, "\nHighest score:", max_score, "\nLowest score:", min_score, "\nRange of scores:", score_range)
            print("Mode(s):", mode)
            for line_num in range(len(stu_ans) + 1):
                print(format(line_num, ">2d"), end='  ')
                if line_num in unique_scores:
                    multiplier = count[unique_scores.index(line_num)]
                    print("*"*multiplier)
                else:
                    print("")
            
    elif op == "q":
        #get info about quizzes
        myfile = open("quizzes.txt", "r")
        data = myfile.read()
        myfile.close()

        lines = data.split("\n")

        for line in lines:
            info = line.split(",") #each string has now been split into a list with two items each
            print(info[0], "has", len(info[1]), "questions")

    else:
        print("Unknown command, try again")
