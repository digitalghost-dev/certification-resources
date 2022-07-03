# Certification Resources

I created this repository to list out the preparation resouces I used for each exam. I hope these help you pass your exam.

## Google Cloud: Associate Cloud Engineer
<sup>Started stuyding: June 5th, 2022; Passed July 1st, 2022</sup>
*note: I have about 3 years of IT support experience and have built a Cloud Run application on Google Cloud so I have some experience/knowledge of these tools.*

First off, I recommend taking a look at the [overview page](https://cloud.google.com/training/cloud-infrastructure#cloud-engineer-learning-path) for the exam on Google's website if you haven't already. This will help you get a good understanding of what to expect on the exam.

Here is the [exam guide](https://cloud.google.com/certification/guides/cloud-engineer).

### Resources Used
* I primarily used the [Cloud Engineer Learning Path](https://www.cloudskillsboost.google/paths/11) as my main learning source. It covers everything you need to know.
  * There are labs that let you get hands-on experience which I think is very beneficial. You can get a 30-day free trial and cancel before it charges you. You also have the option of purchasing individual credits for the labs. The videos are always free.
  * I skipped the following courses/quests:
    * Reliable Google Cloud Infrastructure: Design and Process
    * Automating Infrastructure on Google Cloud with Terraform
    * Logging, Monitoring and Observability in Google Cloud (I completed a few lessons from here but I don't think the entire course is necessary).
* [Udemy practice tests](https://www.udemy.com/course/google-certified-associate-cloud-engineer-practice-exams-gcp/)
  * These practice tests are great. They mimic the real test environment and even had some questions from the actual exam. 
* [gcloud commands cheat sheet](https://cloud.google.com/sdk/docs/images/gcloud-cheat-sheet.pdf)
  * There are questions that require you to know `gcloud`, `gsutil`, and `kubectl` commands.
    * `gsutil` and `kubectl` commands are only used for interacting with Cloud Storage and Kubernetes, respectively. 
* [Developer cheat sheet](https://googlecloudcheatsheet.withgoogle.com/)

### Tips
* Read each question carefully. The verbiage used is precise and if not read carefully, an incorrect answer may seem correct. 
  * For example, the question may state that _**in the future**_ you will need to provision a VM. Possible answers will state to edit the _**current**_ VM but how can you edit a VM that is yet to exist?
  * Even though the possible answer has a correct solution in the event of it existing, it doesn't solve what the question is truly asking.
