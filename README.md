# services-with-python-on-linux
import subprocess

def all_services():
    try:
        status_output = subprocess.run(['service', '--status-all'], capture_output=True, text=True, check=True)
        print(status_output.stdout)
    except subprocess.CalledProcessError as e:
        print(f'An error occured: {e}')

all_services()

def active_services():
    try:
        status_output = subprocess.run(['service', '--status-all'], capture_output=True, text=True, check=True)

        filtred_output = subprocess.run(['grep', r'\[ + \]' ], input=status_output.stdout, capture_output=True, text=True, check=True)

        lines_with_services = subprocess.run(['awk', r'{print $4}'], input=filtred_output.stdout, capture_output=True, text=True, check=True)
        print(lines_with_services.stdout)
    except subprocess.CalledProcessError as e:
        print(f'An error occured: {e}')

#active_services()

def inactive_services():
    try:
        status_output = subprocess.run(['service', '--status-all'], capture_output=True, text=True, check=True)

        filtred_output = subprocess.run(['grep', r'\[ - \]' ], input=status_output.stdout, capture_output=True, text=True, check=True)

        lines_with_services = subprocess.run(['awk', r'{print $4}'], input=filtred_output.stdout, capture_output=True, text=True, check=True)
        print("To są wszystkie  wyłączone usługi na serwerze" + lines_with_services.stdout)
    except subprocess.CalledProcessError as e:
        print(f'An error occured: {e}')

inactive_services()
