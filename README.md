# clone
git clone https://github.com/manigourav19/assignment-gp.git
cd assignment-gp

# create virtual env (Linux/Mac)
python3 -m venv .venv
source .venv/bin/activate

# create virtual env (Windows)
python -m venv .venv
.venv\Scripts\activate

# install dependencies
pip install -r requirements.txt

# run tests
pytest -q

# run an example (fizzbuzz)
python -c "from assignment_gp.task1_fizzbuzz import fizz_buzz_gp; print(fizz_buzz_gp(15))"
