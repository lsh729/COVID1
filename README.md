# COVID1

def normalize_data(n_cases, n_people, scale):
    # Calculate the number of cases per its population
    norm_cases = []
    for idx, n in enumerate(n_cases):
        norm_cases.append(n / n_people[idx] * scale)
    return norm_cases

regions = ['Seoul', 'Gyeongi', 'Busan', 'Gyeongnam', 'Incheon', 'Gyeongbuk', 
           'Daegu', 'Chungnam', 'Jeonnam', 'Jeonbuk', 'Chungbuk', 'Gangwon', 
           'Daejeon', 'Gwangju', 'Ulsan', 'Jeju', 'Sejong']
n_people = [9550227, 13530519, 3359527, 3322373, 2938429, 2630254, 
            2393626, 2118183, 1838353, 1792476, 1597179, 1536270, 
            1454679, 1441970, 1124459, 675883, 365309]  # 2021-08
n_covid = [644, 529, 38, 29, 148, 28, 41, 62, 23, 27, 27, 33, 
            16, 40, 20, 5, 4]  # 2021-09-21

# Calculate the total population and total new cases
sum_people = sum(n_people)
sum_covid = sum(n_covid)

# Normalize new cases per million people
norm_covid = normalize_data(n_covid, n_people, 1000000)

# Print population by region
print('### Korean Population by Region')
print('* Total population:', sum_people)
print()  # Print an empty line
print('| Region  | Population  | Ratio (%) | Cases per 1 million |')
print('|---------|-------------|-----------|---------------------|')

for idx, pop in enumerate(n_people):
    ratio = (n_covid[idx] / pop) * 100  # Calculate ratio of new cases
    print('| {:<6} | {:>10,} | {:>7.2f} | {:>20.2f} |'.format(regions[idx], pop, ratio, norm_covid[idx]))

print()
# Print COVID-19 new cases by region
print('### COVID-19 New Cases by Region')
print('| Region  | New Cases    |')
print('|---------|--------------|')
for idx, cases in enumerate(n_covid):
    print('| {:<6} | {:>12,} |'.format(regions[idx], cases))
